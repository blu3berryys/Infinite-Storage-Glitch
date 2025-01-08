# Infinite-Storage-Glitch (ISG)

**"I was working on this instead of my finals, hope you appreciate it."**

<a href="https://www.buymeacoffee.com/HistidineDwarf" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-red.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>

---

## Introduction

Treat this less like the next Dropbox and more like a "party trick" or a set of techniques to pass data through compression. I do **not** endorse high-volume use of this tool, and I will **not** be approving more commits to make it more convenient. There are several bugs that limit its use, such as poor memory management, which restricts the file size to about **100MB**. These bugs will remain unfixed unless you decide to tackle them yourself.

If YouTube sends me a Cease and Desist, I’ll gladly shut this down.

---

## About ISG

![ezgif com-gif-maker](https://user-images.githubusercontent.com/96934612/219563410-7728447d-5482-41ae-a3ff-cf8446e16ab7.gif)

**Infinite-Storage-Glitch (ISG)** is a tool that lets you embed files into video and upload them to YouTube as storage. It was written entirely in **Rust** (my beloved language).

This project is heavily inspired by:
- [Suckerpinch's "Harder Drive"](https://www.youtube.com/watch?v=JcJSW7Rprio)
- [Discord as a filesystem](https://github.com/pixelomer/discord-fs)

**Note:** Currently, there is no filesystem functionality.

---

## Frequently Asked Questions

### **But is this against YouTube's TOS?**

<details>
<summary><b>Answer:</b> Probably?</summary>

I don't speak legalese. Depending on how YouTube interprets "autogenerated content that computers post without regard for quality or viewer experience" (from their [Community Guidelines](https://support.google.com/youtube/answer/2801973?hl=en#)), this could be a violation. Their TOS also mention circumventing the service, which this tool might do.

**Use at your own risk**. I don’t advise using this tool for anything serious or large. YouTube may understandably get upset, even if the videos are set to "unlisted". Treat this less like a cloud storage solution and more like a party trick.
</details>

---

## Installation

### 1. **Building from Source (Manual Installation)**

> **Warning:** Building from source requires **a lot of CPU and RAM** usage.

#### Prerequisites:
- [Rust](https://www.rust-lang.org/tools/install)
- [OpenCV](https://github.com/twistedfall/opencv-rust)

#### Additional Dependencies (if needed):
- [FFmpeg](https://ffmpeg.org/)
- [Clang](https://clang.llvm.org/)
- [Qt](https://github.com/qt)

#### Steps:
1. Clone this repository:
   ```bash
   git clone https://github.com/your-repo/Infinite-Storage-Glitch.git
   ```

2. Navigate to the repository:
   ```bash
   cd Infinite-Storage-Glitch
   ```

3. Build the project:
   ```bash
   cargo build --release
   ```

4. After building, the executable will be in the `target/release` directory. Run the program:
   ```bash
   ./isg_4real
   ```

### 2. **Using Docker (Easiest Way)**

If you don't want to mess with building dependencies, Docker is your friend. Here's how you can do it:

1. Install [Docker](https://docs.docker.com/get-docker/).
2. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/Infinite-Storage-Glitch.git
   ```
3. Change into the repository directory:
   ```bash
   cd Infinite-Storage-Glitch
   ```

4. Build the Docker image:
   ```bash
   docker build -t isg .
   ```

5. Build the project inside the container:
   ```bash
   docker run -it --rm -v ${PWD}:/home/Infinite-Storage-Glitch isg cargo build --release
   ```

6. The executable will be found in the `target/release` directory. You can run it like so:
   ```bash
   docker run -it --rm -v ${PWD}:/home/Infinite-Storage-Glitch isg ./target/release/isg_4real
   ```

> **Note:** This will generate a Linux binary. If you're on Windows, you can run it via [WSL](https://docs.microsoft.com/en-us/windows/wsl/install-win10) or by using PowerShell with Docker.

---

## How to Use ISG

1. **Prepare your files**:
   - Archive the files you want to upload into a ZIP file.

2. **Run the executable**:
   - Use the `embed` option to embed the ZIP archive into a video file.
   - **Warning:** The video will be significantly larger than the original ZIP file (approximately 4x larger with optimal compression).

3. **Upload to YouTube**:
   - Upload the video to your YouTube channel. It's advisable to keep the video **unlisted**.

4. **Download the video**:
   - Use the `download` option to retrieve the video.

5. **Dislodge the files**:
   - Use the `dislodge` option to extract your original files from the video.

6. **Enjoy!** Now you have a workaround for storing files on YouTube.

![2023-02-16_22-12](https://user-images.githubusercontent.com/96934612/219563769-c05370e9-3f40-406a-85b8-eca14a118be8.png)

---

## Demo

**Warning: Flashing lights!** Watch the demo video here: [YouTube Link](https://www.youtube.com/watch?v=8I4fd_Sap-g)

> Try to use the program on this video and find the files hidden inside.  
> ***No, it’s not just a Rick Roll.***

---

## Explanation for Nerds

The basic principle behind ISG is simple: all files are made of bytes, and bytes can be interpreted as numbers ranging from 0 to 255. These numbers can be represented as colors in pixels using two main modes:

### **1. RGB Mode (Cooler Mode)**
Each byte is stored in one of the three color channels (RGB) of a pixel. This method is efficient and quick, allowing 3 bytes to be stored per pixel.

### **2. Binary Mode (More Robust)**
Due to YouTube's brutal compression algorithms, RGB data is more vulnerable to corruption. In **binary mode**, each pixel is either bright (representing a 1) or dark (representing a 0). We string these binary digits together to form bytes and continue until we run out of data.

### **Compression Considerations**
Both modes are susceptible to corruption by compression. To combat this, the pixels are sized to reduce compression effects. In binary mode, **2x2 blocks** of pixels work best.

### **Settings in Video**
To make the program easier for the user, we include the relevant settings (compression method, pixel size, etc.) in the first frame of the video. This allows the program to auto-detect how to extract the data, removing the need for the user to remember complex settings.

---

## Final Comments

I welcome any and all feedback, especially constructive critiques of the code! Feel free to use this tool however you want, but **credit would be much appreciated**. If you encounter any issues, you can contact me over Discord.
