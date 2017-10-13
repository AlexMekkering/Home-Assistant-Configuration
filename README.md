# Home-Assistant-Configuration
My main Home Assistant configuration

# Installation instructions

## Installation of required Arch Linux packages
```bash
# make for Z-Wave and automake/autoconf for Tradfri
sudo pacman -Syu --needed git python gcc sed grep autoconf automake make
```

##  Setting up Python virtualenv
```bash
python -m venv venv
source venv/bin/activate

pip install -U pip setuptools wheel cython homeassistant
```

## Tradfri
```bash
git clone --depth 1 https://git.fslab.de/jkonra2m/tinydtls.git
cd tinydtls
mv configure.in configure.ac
autoreconf
./configure --with-ecc --without-debug
cd cython
python setup.py install

cd ../..

git clone https://github.com/chrysn/aiocoap
cd aiocoap
git reset --hard 3286f48f0b949901c8b5c04c0719dc54ab63d431
python -m pip install -U .

cd ..
rm -rf tinydtls aiocoap
deactivate
```
