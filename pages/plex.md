# Plex

Brief overview

The settings I use


## Server

Intel NUC 📡


NUC8i5BEK


### Choosing a server

Final choice: NUC8i5BEK


Chose 8 because it had outsized power at the 5 point.

Intel scaled this back and made the 3/5/7 more balanced

Rationale for short one (also talks about ram choices): [https://www.reddit.com/r/intelnuc/comments/a4xs6m/nuc8i5beh_or_nuc8i5bek/ebn5nsy/?utm_source=share&utm_medium=ios_app&utm_name=iossmf&context=3](https://www.reddit.com/r/intelnuc/comments/a4xs6m/nuc8i5beh_or_nuc8i5bek/ebn5nsy/?utm_source=share&utm_medium=ios_app&utm_name=iossmf&context=3) 

Rational for 1tb instead of 2tb or tall with 2.5 sata (you can always plugin a slim hdd):  [https://www.reddit.com/r/intelnuc/comments/99b89l/nuc_with_high_capacity_25_hdd/e4mm8h3/?utm_source=share&utm_medium=ios_app&utm_name=iossmf&context=3](https://www.reddit.com/r/intelnuc/comments/99b89l/nuc_with_high_capacity_25_hdd/e4mm8h3/?utm_source=share&utm_medium=ios_app&utm_name=iossmf&context=3) 

Compatibility:  [https://www.crucial.com/compatible-upgrade-for/intel/nuc8i5bek](https://www.crucial.com/compatible-upgrade-for/intel/nuc8i5bek) 

Model rational:

* Plex wiki suggests a 2000 passmark score for one 1080p transcode and 4000 for one 4k transcode
* NUC8i5BEH = 4771, multicore = 16943
* NUC8i7BEH = 5147, multicore = 17074
* Get the i5 and 2x 8gb ram
	* cooler and quieter
* Someone  [here](https://www.reddit.com/r/intelnuc/comments/ashcv9/debating_between_nuc8i7beh_nuc8i5beh/)  says: 
	* Get the i5 and get matching RAM sticks for dual channel mode. The premium for 2666 isn’t going to get you much over 2400, but dual channel over single channel is a huge difference.
	* The horsepower difference between the i7 and i5 is only like 12%. I got the i7 myself because I am constantly running handbrake conversions on it so the extra oomph is helpful, but for your use-case it’s tossing out money.



### Choosing a server OS

Try Ubuntu 20.04 Desktop, why not

 [https://www.reddit.com/r/intelnuc/comments/gl1p09/help_intel_nuc_nuc8i5beh_running_ubuntu_2004_lts/](https://www.reddit.com/r/intelnuc/comments/gl1p09/help_intel_nuc_nuc8i5beh_running_ubuntu_2004_lts/) 

* this person used 20.04 (probably server), no problem (on an H instead of the K, same thing) [https://ubuntu.com/download/intel-nuc-desktop](https://ubuntu.com/download/intel-nuc-desktop) 
* they only have their certified ones, which are old, and for the 7, but I have an 8

18.04 of 20.04? Do 20, LTS = stable

Do Desktop version, not Server version. Since it might need Lari debugging. Or it might need me remoting in. And I want a desktop view.

Try server when you’re more accomplished/capable of CLI only interface



Ubuntu 18.04 comes up often (lts long term support)

Ubuntu with Plex in docker, hardware encoding still possible as long as you map controllers
Proxmox mentioned but seems overkill currently, full details here  [https://jackcuthbert.dev/blog/intel-nuc-gpu-passthrough-in-proxmox-plex-docker/](https://jackcuthbert.dev/blog/intel-nuc-gpu-passthrough-in-proxmox-plex-docker/) 


### Setting up remote on the server

Tried this:
 [https://askubuntu.com/questions/1089053/cannot-share-desktop-18-04-1-lts](https://askubuntu.com/questions/1089053/cannot-share-desktop-18-04-1-lts) 
> gsettings set org.gnome.Vino require-encryption false
It worked!

Next step would be remote access outside the network, and actual security




Remote VNC from Big Sur to Ubuntu  [https://thedevopslife.com/osx-big-sur-vnc-to-ubuntu/](https://thedevopslife.com/osx-big-sur-vnc-to-ubuntu/) 
This says to do exactly what I struggled through, installing vino and disabling encryption


Ok so next step is learning about SSH tunneling






## Getting Media

youtube-dl

Full Channel Command:
youtube-dl —format bestvideo+bestaudio/best —download-archive archive.txt —merge-output-format mp4 —ignore-errors —all-subs —embed-subs —add-metadata —write-thumbnail —write-annotations —write-info-json  —write-description —output “%(uploader)s/%(upload_date)s %(title)s %(id)s.%(ext)s” —yes-playlist  [https://www.youtube.com/channel/UCUEtRQBZXbZDRCBCt_Cc3Zg](https://www.youtube.com/channel/UCUEtRQBZXbZDRCBCt_Cc3Zg) 

Single Video Command:
youtube-dl —format bestvideo+bestaudio/best —download-archive archive.txt —merge-output-format mp4 —ignore-errors —all-subs —embed-subs —add-metadata —write-thumbnail —write-annotations —write-info-json  —write-description —output “%(uploader)s/%(upload_date)s %(title)s %(id)s.%(ext)s”  [https://www.youtube.com/watch?v=loVXsvtpWHU](https://www.youtube.com/watch?v=loVXsvtpWHU) 





Source:  [https://www.reddit.com/r/DataHoarder/comments/ahwehz/how_to_archive_a_youtube_channel/](https://www.reddit.com/r/DataHoarder/comments/ahwehz/how_to_archive_a_youtube_channel/) 


In Practice:

The above command will not stop on errors, so if you run it, search the output for “error”


Breakdown:

*youtube-dl*

*—format bestvideo+bestaudio/best*
Video format code, see the “FORMAT SELECTION” for all the info

*—download-archive archive.txt*
Download only videos not listed in the archive file. Record the IDs of all downloaded videos in it.

*—merge-output-format mkv*
 If a merge is required (e.g. bestvideo+bestaudio), output to given container format. One of mkv, mp4, ogg, webm, flv. Ignored if no merge is required

*—ignore-errors*
Continue on download errors, for example to skip unavailable videos in a playlist

*—all-subs*
Download all the available subtitles of the  video

*—embed-subs*
Embed subtitles in the video (only for mp4, webm and mkv videos)

*—add-metadata*
Write metadata to the video file

*—write-thumbnail*
Write thumbnail image to disk

*—write-annotations*
Write video annotations to a .annotations.xml file

*—write-info-json*
Write video metadata to a .info.json file

*—write-description*
Write video description to a .description file

*—o “%(uploader)s/%(title)s %(id)s.%(ext)s”*
Output filename template, see the “OUTPUT TEMPLATE” for all the info

*—yes-playlist* [https://www.youtube.com/channel/UCUEtRQBZXbZDRCBCt_Cc3Zg](https://www.youtube.com/channel/UCUEtRQBZXbZDRCBCt_Cc3Zg) 
Download the playlist, if the URL refers to a video and a playlist.
