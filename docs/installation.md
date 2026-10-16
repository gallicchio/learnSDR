# Installing the Software

These lessons use [GNU Radio](https://www.gnuradio.org) **3.10** and its graphical editor, GNU Radio Companion (GRC). The flowgraphs in this repository were last tested in October 2026 with GNU Radio 3.10.12 on Ubuntu 26.04 LTS. They should open in any GNU Radio 3.10.x; they will *not* open in the old 3.8 series that the videos were recorded with (the blocks are the same, the file format changed a little).

Besides GNU Radio itself you need the driver blocks for the hardware:

| Hardware | GRC block | Software that provides it |
| --- | --- | --- |
| RTL-SDR (Lesson 1 onward) | **RTL-SDR Source** | `gr-osmosdr` + `librtlsdr` |
| ADALM-PLUTO (Lesson 8 onward) | **PlutoSDR Source / Sink** | `gr-iio` (part of GNU Radio 3.10) + `libiio` |
| USRP B210 (only the [Spectrum Demo](SpectrumDemo.md)) | **UHD: USRP Source** | `uhd` + its FPGA images |

## Ubuntu Linux (recommended)

On a current Ubuntu LTS (24.04 or 26.04) everything comes from the standard repositories:

```bash
sudo apt install gnuradio gr-osmosdr rtl-sdr libiio-utils soapysdr-module-all gqrx-sdr
```

Then, one-time setup for each piece of hardware:

```bash
# RTL-SDR: stop the kernel's DVB-T TV driver from grabbing the dongle
echo 'blacklist dvb_usb_rtl28xxu' | sudo tee /etc/modprobe.d/blacklist-rtlsdr.conf
sudo rmmod dvb_usb_rtl28xxu 2>/dev/null
rtl_test -t          # should find "Realtek, RTL2838UHIDIR" and the R820T/R828D tuner

# PlutoSDR: it shows up as a USB network adapter at 192.168.2.1 (nothing to install)
iio_info -s          # should list "PlutoSDR" at ip:192.168.2.1 and usb:...

# USRP (optional): download the FPGA/firmware images once
sudo uhd_images_downloader
uhd_find_devices
```

Log out and back in once after installing so your user picks up the `plugdev` group permissions from the udev rules. Then start GRC from the application menu or with `gnuradio-companion`.

## Windows

Install [radioconda](https://github.com/ryanvolz/radioconda) (a ready-made GNU Radio distribution; download the `.exe` installer from its Releases page). It includes GNU Radio 3.10 with the RTL-SDR (`gnuradio-osmosdr`), PlutoSDR (`gnuradio-iio`/`libiio`) and USRP (`uhd`) blocks. Two drivers have to be installed by hand:

- **RTL-SDR:** plug in the dongle, run [Zadig](https://zadig.akeo.ie/), choose *Bulk-In, Interface (Interface 0)* and install the **WinUSB** driver.
- **PlutoSDR:** install the [PlutoSDR-M2k USB drivers](https://github.com/analogdevicesinc/plutosdr-m2k-drivers-win/releases) so the Pluto appears as a network device at 192.168.2.1.

Launch *GNU Radio Companion* from the Start menu entry that radioconda creates.

## macOS

Install [radioconda](https://github.com/ryanvolz/radioconda) using the `.pkg` for your Mac (Intel or Apple Silicon). The PlutoSDR needs no driver: it appears as a USB network interface at 192.168.2.1. The RTL-SDR works out of the box through radioconda on Apple Silicon; on Intel Macs you may need `brew install librtlsdr` as well.

## Getting the flowgraphs

```bash
git clone https://github.com/gallicchio/learnSDR.git
cd learnSDR
gnuradio-companion lesson01b_RTL_SDR_FM.grc
```

Every lesson page links to its `.grc` file(s). In GRC, press the "play" button (or F6) to generate and run a flowgraph; GRC writes a `.py` file next to the `.grc`.

## Troubleshooting

- **`usb_claim_interface error -6`** when starting an RTL-SDR flowgraph: the DVB-T kernel driver still owns the dongle (Linux), or another flowgraph is still running. Close other flowgraphs; see the blacklist step above.
- **`[R82XX] PLL not locked!`** from the RTL-SDR is harmless.
- **PlutoSDR not found:** check `iio_info -s` (Linux/macOS) or that you can `ping 192.168.2.1`. The *IIO context URI* field of the Pluto blocks can be left blank to auto-detect, or set to `ip:192.168.2.1`. If your Pluto is on an older firmware, update it following the [Analog Devices instructions](https://wiki.analog.com/university/tools/pluto/users/firmware).
- **The Pluto transmits nothing, although the flowgraph runs:** if some *other* program (e.g. SoapySDR/osmosdr, SDR++, gqrx) used the Pluto's transmitter, it may leave the TX local oscillator powered down, and the GNU Radio PlutoSDR Sink does not turn it back on. Either power-cycle the Pluto or run `iio_attr -u ip:192.168.2.1 -c -o ad9361-phy altvoltage1 powerdown 0`.
- **A block is red / "FFT Size should be a power of 2":** GNU Radio 3.10 insists that the QT GUI Frequency Sink FFT size is a power of two (1024, 4096, ...).
- **"Endianness: gr.GR_MSB_FIRST cannot be evaluated":** add an *Import* block containing `from gnuradio import gr`. (The flowgraphs in this repository already do this.)
- **The flowgraph is sluggish or shows "D" (dropped samples)** in the console: disable some of the QT GUI sinks you are not looking at, or lower the sample rate.
