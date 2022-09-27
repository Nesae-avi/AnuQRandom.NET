# AnuQRandom.Net
A .NET 6 library for accessing the ANU quantum random number generator API located at: https://quantumnumbers.anu.edu.au

How to use:

```C#
var client = new AnuQRandom.NewApiClient("[API KEY]");
var data = await client.RequestAsync();

if (data != null && data.Success)
{
	foreach (var number in data.Data)
	{
		Console.WriteLine(number);
	}
}
```

To use the old API create an instance of the `OldApiClient` class instead.

Use properties to set custom values for `Block Size`, `Array Length` and `Data Type`:
```C#
var client = new AnuQRandom.OldApiClient
{
	DataType = AnuQRandom.RequestedDataType.hex16,
	BlockSize = 0x10,
	ArrayLength = 0x22
};
```

Create an instance of the `DirtyClient` class to access website - provided functionality that is not a part of the official API:
```C#
var client = new AnuQRandom.DirtyClient();

// Save a random 256 x 256 scatter plot image in the current application working directory.

await client.GetScatterPlotImageAsync("scatter_plot.png");

var hexBlock = await client.GetHexadecimalBlockAsync();
var binBlock = await client.GetBinaryBlockAsync();
var alpBlock = await client.GetAlphanumericBlockAsync();

Console.WriteLine("Hexadecimal block:\n\n");
Console.WriteLine(hexBlock);

Console.WriteLine("\n\nBinary block:\n\n");
Console.WriteLine(binBlock);

Console.WriteLine("\n\nAlphanumeric block:\n\n");
Console.WriteLine(alpBlock);
```
