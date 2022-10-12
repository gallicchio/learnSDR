# Installing the necessary software

[GNU Radio](https://www.gnuradio.org) is a free, open-source radio ecosystem that runs primarily on Linux systems, although there are versions compiled for other operating systems.

In 2022, we run GNURadio 3.10 on [Ubuntu 22.04 LTS (Jammy Jellyfish)](https://www.releases.ubuntu.com/22.04/). After installing, rnu 

  ```sudo apt-get install gnuradio rtl-sdr gqrx-sdr soapysdr-module-all```


In 2021, we ran GNURadio 3.8 on [Ubuntu 21.04 (Hirsute Hippo)](https://www.releases.ubuntu.com/21.04/). 
After installing Ubuntu, issue the following, which will install more libraries than are strictly necessary:



  ```sudo apt-get install gnuradio gqrx-sdr cubicsdr inspectrum 
   hackrf hacktv soapysdr-module-all rtl-sdr gnss-sdr rtklib rtklib-qt libiio-dev libiio-utils python3-libiio flatpak limesuite multimon multimon-ng gpredict python3-orbit-predictor gr-osmosdr gr-limesdr gr-fosphor gr-iio```


Previous versions of Ubuntu did not include libraries for the PlutoSDR hardware.

You should now have GNU Radio installed. Click on the GNU Radio icon to launch it.

<p class='center' markdown='0'>
  <img src='figs/gnuradio-icon.png' alt='alt text'>
</p>

