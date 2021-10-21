# Installing the necessary software

[GNU Radio](https://www.gnuradio.org) is a free, open-source radio ecosystem that runs primarily on Linux systems, although there are versions compiled for other operating systems. We are currently running version 3.8 on [Ubuntu 21.04 (Hirsute Hippo)](https://www.releases.ubuntu.com/21.04/), for which the installation of GNU Radio is much simpler than on previous version of Ubuntu.

After installing Ubuntu 21.04, issue the following
   > sudo apt-get install gnuradio gqrx-sdr cubicsdr inspectrum 
   >   hackrf hacktv soapysdr-module-all rtl-sdr gnss-sdr rtklib rtklib-qt libiio-dev libiio-utils python3-libiio flatpak limesuite multimon multimon-ng gpredict python3-orbit-predictor gr-osmosdr gr-limesdr gr-fosphor gr-iio

You should now have GNU Radio installed. Click on the GNU Radio icon  to launch it.
<p class='center' markdown='0'>
  <img src='figs/gnuradio-icon.png' alt='alt text'>
</p>

