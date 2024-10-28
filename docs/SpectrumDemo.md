# Spectrum Analyzer Demo with USRP SDRs

This isn't exactly another lesson, but a demo of using python directly with the Ettus UHD library to quickly take spectra and recordings.

<iframe width="560" height="315" src="https://www.youtube.com/embed/olqedEtaVZI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The jupyter-lab notebook is at [https://github.com/gallicchio/learnSDR/blob/main/SpectrumDemo.ipynb](https://github.com/gallicchio/learnSDR/blob/main/SpectrumDemo.ipynb)

## My hardware

* I started development on the hardware I've got:
    - USRP B210 USB 3.0: 70 MHz (or 50 MHz) - 6 GHz; (61.44MS/s quadrature) Gain: 0.0 to 76.0 step 1.0 dB; Analog BW: 0.2 - 56 MHz
    - USRP X310 with TwinRX daughterboards: 10 MHz - 6 GHz; Gain: 0-93dB; Analog Bandwidth 80 MHz
    - USRP X310 with UBX-160 daughterboards: 10 MHz - 6 GHz; Gain: 0.0 to 31.5 step 0.5 dB; Analog Bandwidth fixed at 160 MHz


## Getting started on USRP X310 in general

From `https://files.ettus.com/manual/page_usrp_x3x0.html`

```
It's SFP+ port 0 is configured for 1 GbE by default (HG firmware) and 10 GbE if you load the XG firmware. SFP+ port 1 is always 10 GbE.
It defaults to static IP address 192.168.10.2 
You should connect directly to it (ethernet to ethernet) with a static ethernet configuration on the laptop. Turn off any VPN.
The host should be (Address) 192.168.10.1 with static subnet mask (Netmask) 255.255.255.0 with no Gateway or DNS or Routes
ping 192.168.10.2  # Port 0 (default HG Image) 1 GbE
ping 192.168.30.2  # Port 0 (alternate XG Image) 10 GbE
ping 192.168.40.2  # Port 1 (either HG/XG Image) 10 GbE
uhd_find_devices  # shows up as X300 even if it's X310
uhd_usrp_probe
uhd_usrp_probe --args addr=192.168.10.2
uhd_usrp_probe --args "type=x300"  # even if it's an X310
To update or change firmware:
sudo uhd_images_downloader
# Even though it's an x310, only the type x300 is recognized. It should do the right thing with that, but I'm not sure.
uhd_image_loader --args="type=x300,addr=192.168.10.2" --fpga-path="/usr/share/uhd/images/usrp_x310_fpga_HG.bit"  # default image

Only AFTER things are working and you want to start squeezing the network interface to the max, try:

See the transport application notes on buffer resizing. Run
sudo sysctl -w net.core.wmem_max=2426666

Increase the Ethernet maximum transmission unit (MTU) size from 1500 (default to hop through routers)
  up to 9000 ("Jumbo Frame") for a 5% speed bump due to less header overhead
See https://en.wikipedia.org/wiki/Jumbo_frame
From https://www.baeldung.com/linux/maximum-transmission-unit-change-size
ip a      # list the interfaces and find the one of interest
ifconfig  # list the interfaces and find the one of interest
Check the current mtu:
ip a | grep mtu
Temporarily Change the one connected to the USRP X310 to 9000
sudo ip link set dev enp3s0f0np0 mtu 9000  # szilard
sudo ip link set dev enp21s0f0np0 mtu 9000  # bell
ip a | grep mtu
To do a permenant change that survives reboot:

```

## python code rather than GNUradio

See <https://pysdr.org/content/usrp.html>

## Installing for jupyterlab

```
pip3 install jupyterlab ipympl jupyter notebook matplotlib ipython bokeh jupyter_bokeh


jupyter-lab --ip IP_ADDRES_TO_SERVE_FROM
# It'll tell you where to point the browser.

Better, just run jupyter-lab and set up an ssh tunnel:

See the transport application notes on buffer resizing.
Please run: sudo sysctl -w net.core.wmem_max=24862979
```

