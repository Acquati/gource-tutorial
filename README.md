# Project development visualization whit [Gource](https://gource.io/)

### [Gource](https://gource.io/) offers a great way to visualize the progress of your project versioned by [Git](https://git-scm.com/)

[![Gource in Bloom](https://img.youtube.com/vi/NjUuAuBcoqs/0.jpg)](http://www.youtube.com/watch?v=NjUuAuBcoqs)

## Instalation

### Mac

```
brew install gource
```

### Linux

Download the file gource-0.49.tar.gz at https://gource.io/

Extract and open the directory:

```
tar -xvzf ~/Downloads/gource-0.49.tar.gz -C ~/Documents

cd ~/Documents/gource-0.49
```

On the created directory, follow the commands to install and make gource command global:

```
sudo apt-get -y update

sudo apt-get install -y libsdl2-dev libsdl2-image-dev libpcre3-dev libfreetype6-dev libglew-dev libglm-dev libboost-filesystem-dev libpng12-dev libsdl1.2-dev libsdl-image1.2-dev libtinyxml-dev

./configure --prefix=/usr/local/gource/0.49

make

sudo make install

cd /usr/bin

sudo ln -s /usr/local/gource/0.49/bin/gource
```

## Visualization

Now that gource is installed, go to a project directory that have a .git file and run the command, lets see the project whit some nice gource options:

```
gource --max-files 1500 --key -f --highlight-users --filename-time 3 --output-framerate 25 -s 0.6 --multi-sampling --auto-skip-seconds .1
```

## Making a .mp4 video

First, lets install [ffmpeg](https://www.ffmpeg.org/) to covert ower video to .mp4

### Mac

```
brew install libvpx

brew install ffmpeg --with-libvpx
```

### Linux

```
sudo apt-get -y install ffmpeg
```

Now we will generate a gource.ppm file from ower currently visualization:

```
gource --max-files 1000 --key -800x600 --highlight-users --filename-time 3 --output-framerate 25 -s 0.6 --multi-sampling --auto-skip-seconds .1 --stop-at-end --hide mouse,progress -o gource.ppm
```

And then whit ffmpeg we will convert the gource.ppm file into gource.mp4 file:

```
ffmpeg -y -r 15 -f image2pipe -vcodec ppm -i gource.ppm -vcodec libx264 -preset medium -pix_fmt yuv420p -crf 1 -threads 0 -bf 0 gource.mp4
```

The gource.mp4 file will be generated in the directory of the project and can be moved to somewhere else, have fun!

If the file gets too large, use ffmpeg to reduce the file size, an output.mp4 file will be generated:

```
ffmpeg -i gource.mp4 -c:v libx264 -crf 19 -level 3.1 -preset slow -tune film -filter:v scale=-1:720 -sws_flags lanczos -c:a libfdk_aac -vbr 5 output.mp4
```

## References

https://superuser.com/questions/582198/how-can-i-get-high-quality-low-size-mp4s-like-the-lol-release-group

http://tylerfrankenstein.com/code/install-gource-ubuntu-1010-visualize-git-repo

https://gist.github.com/miguelsaddress/e88384d135ce80866d6a

https://github.com/acaudwell/Gource/wiki/Videos

https://gist.github.com/qiaoxueshi/5910150

https://www.ffmpeg.org/

https://git-scm.com/

https://gource.io/
