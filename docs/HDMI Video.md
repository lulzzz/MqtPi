# Raspberry Video Playout

#disable tty:
#sudo systemctl -a | grep tty
#sudo systemctl stop getty@tty1.service
#sudo systemctl daemon-reload
#sudo systemctl disable getty@tty1.service

sudo systemctl enable getty@tty1.service

 
sudo crontab -e
add:
@reboot sleep 10 && /usr/bin/fbi -T 1 /home/pi/ww_black.png --noverbose
@reboot sleep 30 && /usr/bin/fbi -T 1 /home/pi/ww_black.png --noverbose


sudo apt-get install cutycapt 
sudo apt-get install xvfb 
xvfb-run --server-args="-screen 0, 1280x1200x24" cutycapt --url=http://jonajona.nl --out=jonass.png


xvfb-run --server-args="-screen 0, 1280x1024x24" cutycapt --url=http://jonajona.nl/dash.php --min-width=1280 --min-height=1024 --out=jonass.png && sudo /usr/bin/fbi -T 1 /home/pi/jonass.png --noverbose 
xvfb-run --server-args="-screen 0, 1280x1024x24" cutycapt --url=http://jonajona.nl --min-width=1280 --min-height=1024 --out=jonass.png && sudo /usr/bin/fbi -T 1 /home/pi/jonass.png --noverbose

### **Display Video**:
sudo fbi -T 1 ww_black.png --noverbose
>`sudo apt-get install fbi` to install fbi
><br>`sudo fbi -T 1 ww+.png --noverbose` to show PNG image (as background, no line)
><br>`sudo killall fbi` to clear all images
><br>`omxplayer -o hdmi small.mp4` to display MP4 file
 
### **Display cool Video**: (fade-in-out)
>` sudo apt-get install ffmpeg` to install ffmpeg
><br>`sudo fbi -T 1 ww+.png --noverbose` to show PNG image (as background, no line)
><br>To fade in from black, starting at frame 0, over 50 frames (2 seconds @ 25fps):
><br>`ffmpeg -i input.mp4 -filter:v 'fade=in:0:50' -c:v libx264 -crf 22 -preset veryfast -c:a copy output.mp4` 
><br>To fade out starting at frame 21000 (14 minutes @ 25fps), over 50 frames:
><br>`ffmpeg -i input.mp4 -filter:v 'fade=out:21000:50' -c:v libx264 -crf 22 -preset veryfast -c:a copy output.mp4` 
><br>You can combine the two into a filterchain:
><br>`ffmpeg -i input.mp4 -filter:v 'fade=in:0:50,fade=out:21000:50' -c:v libx264 -crf 22 -preset veryfast -c:a copy output.mp4` 