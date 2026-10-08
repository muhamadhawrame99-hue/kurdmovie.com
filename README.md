using System.Text;
using Whisper.net;

Console.OutputEncoding = Encoding.UTF8;

Console.WriteLine("======================================");
Console.WriteLine("       NOVA MOVIES SUBTITLE AI");
Console.WriteLine("======================================");
Console.WriteLine();

string modelPath = "ggml-base.bin";

if (!File.Exists(modelPath))
{
    Console.WriteLine("Whisper model نییە.");
    Console.WriteLine("Model دادەبەزێنرێت...");

    using var modelStream =
        await WhisperGgmlDownloader.Default.GetGgmlModelAsync(GgmlType.Base);

    using var modelFile = File.Create(modelPath);

    await modelStream.CopyToAsync(modelFile);

    Console.WriteLine("Model بە سەرکەوتوویی دابەزێنرا.");
}

Console.WriteLine();
Console.WriteLine("ڕێگای فایلەکەی فیلم بنووسە:");
Console.WriteLine("نمونە: C:\\Movies\\movie.wav");
Console.WriteLine();

string? audioPath = Console.ReadLine();

if (string.IsNullOrWhiteSpace(audioPath))
{
    Console.WriteLine("هیچ فایلێکت دیاری نەکردووە.");
    return;
}

if (!File.Exists(audioPath))
{
    Console.WriteLine("فایلەکە نەدۆزرایەوە.");
    return;
}

Console.WriteLine();
Console.WriteLine("دەست بە ناسینەوەی دەنگ دەکات...");
Console.WriteLine();

using var whisperFactory = WhisperFactory.FromPath(modelPath);

using var processor = whisperFactory
    .CreateBuilder()
    .WithLanguage("auto")
    .Build();

using var fileStream = File.OpenRead(audioPath);

var subtitles = new List<Subtitle>();

int number = 1;

await foreach (var result in processor.ProcessAsync(fileStream))
{
    string text = result.Text.Trim();

    if (string.IsNullOrWhiteSpace(text))
        continue;

    Console.WriteLine(
        $"[{FormatTime(result.Start)} --> {FormatTime(result.End)}] {text}"
    );

    subtitles.Add(
        new Subtitle
        {
            Number = number++,
            Start = result.Start,
            End = result.End,
            Text = text
        }
    );
}

string outputPath =
    Path.Combine(
        Path.GetDirectoryName(audioPath)!,
        Path.GetFileNameWithoutExtension(audioPath) + "_English.srt"
    );

SaveSrt(subtitles, outputPath);

Console.WriteLine();
Console.WriteLine("======================================");
Console.WriteLine("تەواو بوو!");
Console.WriteLine($"SRT: {outputPath}");
Console.WriteLine("======================================");

static string FormatTime(TimeSpan time)
{
    return $"{(int)time.TotalHours:00}:" +
           $"{time.Minutes:00}:" +
           $"{time.Seconds:00}," +
           $"{time.Milliseconds:000}";
}

static void SaveSrt(
    List<Subtitle> subtitles,
    string path)
{
    var sb = new StringBuilder();

    foreach (var subtitle in subtitles)
    {
        sb.AppendLine(subtitle.Number.ToString());

        sb.AppendLine(
            $"{FormatTime(subtitle.Start)} --> {FormatTime(subtitle.End)}"
        );

        sb.AppendLine(subtitle.Text);

        sb.AppendLine();
    }

    File.WriteAllText(
        path,
        sb.ToString(),
        new UTF8Encoding(false)
    );
}

class Subtitle
{
    public int Number { get; set; }

    public TimeSpan Start { get; set; }

    public TimeSpan End { get; set; }

    public string Text { get; set; } = "";
}
