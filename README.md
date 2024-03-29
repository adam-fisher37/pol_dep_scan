# pol_dep_scan
script to run to automate a polarization dependent spectrograph scan
for use in OSU's Chowdhury lab
by Adam Fisher

currently only supports interfacing with:
Thorlabs TDC001 controller connected to Thorlabs PRM1Z8 motorized waveplate
Thorlabs KDC101 controller connected to Thorlabs PRM1Z8 motorized waveplate
polarizer and the Ocean Optics SpectraPro HRS-300 spectrometer

requires 4 packages: thorlabs_apt_device, pyserial, pylablib, and seabreeze (links below)
APT: https://thorlabs-apt-device.readthedocs.io/en/latest/index.html
Seabreeze: https://python-seabreeze.readthedocs.io/en/latest/index.html
pyserial: https://pyserial.readthedocs.io/en/latest/pyserial.html
PyLabLib: https://pylablib.readthedocs.io/en/stable/index.html
These all have dependencies so read their documentation
both of these packages as well as this one has no relation to their respective companies

### Three ways to use
dual-pol_specscan.py - automates both waveplates and spectrometer, saves data
pol_dep_specscan.py - automates ONLY TDC001 controlled waveplate and spectrometer, saves data
pol_prgm.py - automates ONLY TDC001 controlled waveplate Thorlabs waveplate

### Please read the .py script before running
you must adjust the script to have the desired inputs before running (and save as well) for the program to work
once that is done all you need to do is run the script press enter twice and it will take the measurements and save the data on its own

### the program also takes the background in the beginning
but the background measurement is sandwiched between two user inputs (press enter once ready) so that you can ensure you are ready to take the background measurement and then again so that you are ready to take the full measurement

### how data being saved
data is saved as a .txt file with utf-8 encoding, you are required to set the file name and its destination.

the file name you use MUST NOT be present in the destination directory, if it is you have the option to rename the file

there is a header that has the time the file was created and the array of positions of the polarizer when data was collected [degress]. They have the '#' character in front to be compatible with numpy.loadtxt or numpy.genfromtxt

format: Nx(M+2) array of comma seperated values, [[wvl],[bkg],[I(1st pol pos)],...,[I(ith pol pos)],...,[I(Nth pol pos)]]. where N is the number of data points that the spectrograph collects and M is the number of angles that the polarizer will rotate to, wvl,bkg,I(pos) Nx1 col arrays 