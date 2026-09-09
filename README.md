# Base64 Image Converter

A PowerShell GUI tool for converting images to Base64 and back. Built with Windows Forms, no
dependencies beyond what ships with Windows.

Useful when you need to embed an image in HTML/CSS, stuff one into a JSON payload, or pull an
image back out of a Base64 blob someone sent you.

## Features

- Image to Base64 with optional `data:image/png;base64,` prefix
- Base64 back to an image file (accepts raw Base64 or a full data URL)
- Thumbnail preview of the selected image
- Copy to / paste from clipboard
- Supports JPG, JPEG, PNG, GIF, BMP, TIFF
- 10 MB input limit

## Requirements

- Windows with PowerShell 5.1 (or PowerShell 7 on Windows)
- .NET Windows Forms, which is present by default

PowerShell 7 on Linux or macOS will not work. Windows Forms is Windows-only.

## Installation

Clone or download the script. There is nothing to install.

```powershell
git clone https://github.com/pjhiggins1965/base64-image-converter.git
cd base64-image-converter
```

## Running It

Scripts downloaded from the internet are blocked by default, so you will likely hit an execution
policy error on the first run. Two ways around it:

Unblock the file once and run normally:

```powershell
Unblock-File .\Base64Converter.ps1
.\Base64Converter.ps1
```

Or bypass the policy for just that one invocation, which changes nothing system-wide:

```powershell
powershell.exe -ExecutionPolicy Bypass -File .\Base64Converter.ps1
```

If you want to allow local scripts permanently for your own account:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

## Usage

### Converting an image to Base64

1. Click **Browse** and pick an image. The preview and dimensions appear once it loads.
2. Decide on the **Include data URL prefix** checkbox before converting. Checked gives you
   `data:image/png;base64,AAAA...` which drops straight into an `<img src="">` or a CSS
   `url()`. Unchecked gives you the bare encoded string, which is what most APIs and database
   columns want.
3. Click **Convert to Base64**.
4. Click **Copy to Clipboard**.

The checkbox is read at conversion time, not at browse time. If you toggle it after converting,
click Convert again to regenerate.

### Converting Base64 back to an image

1. Click **Paste from Clipboard**, or type/paste into the text box directly.
2. Click **Save as Image** and choose a location.

The prefix is stripped automatically if present, so you can paste either form. One thing to watch:
the file extension you pick in the save dialog does not convert anything. The bytes are written as
decoded. If the Base64 came from a PNG and you save it as `photo.jpg`, you get a PNG file with the
wrong name on it. Match the extension to whatever the source format actually was.

### Clear

Resets the text box, file path, and preview.

## Known Limitations

- No re-encoding between formats. Bytes in, bytes out.
- The 10 MB cap is there because the text box gets sluggish with very large strings. Base64 runs
  roughly 33% larger than the source file, so a 10 MB image is about a 13.5 MB string.
- No drag and drop yet.
- Fixed window size.

## License

MIT

## Author

pjhiggins - [@pjhiggins1965](https://github.com/pjhiggins1965)
