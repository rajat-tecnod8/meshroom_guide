# meshroom_guide

Create a VM and install appropriate NVIDIA GPU drivers.

```bash
sudo apt-get update
sudo apt install -y nvidia-utils-535
sudo apt-get install -y nvidia-driver-535
sudo reboot
```

Download and install meshroom linux tar package from https://github.com/alicevision/meshroom/releases.

Extract the package
```bash
sudo tar -xvf <package_name>
```

Install ffmpeg for frame extraction
```bash
sudo apt install -y ffmpeg
```

For extracting frames create the following bash file as extract_frames.sh.
```bash
# usage: extract_frames.sh <sequence_name> <full_video_path> <downsample_rate>

data_path=Input/${1}_ds${3}
image_path=${data_path}
mkdir -p ${image_path}
ffmpeg -i ${2} -vf "select=not(mod(n\,$3))" -vsync vfr -q:v 2 ${image_path}/%06d.jpg
```

Now for running meshroom, run the 'meshroom_batch' file in the Meshroom directory.
```bash
sudo ./Meshroom-2023.3.0/meshroom_batch --input <images_folder> --output <output_directory>
```

