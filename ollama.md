# ollama

https://ollama.com

INSTALL ON HOST
```shell
curl -fsSL https://ollama.com/install.sh | sh
```

RADEON RX SETUP (FEDORA)
```shell
sudo dnf install rocm-hip rocm-devel rocm-hip rocm-hip-devel radeontop rocminfo rocm-opencl nvtop

# https://fedoraproject.org/wiki/SIGs/HC
sudo usermod -a -G render,video $LOGNAME
```

LEGACY RADEON 5500/5600 SEUP (OPTIONAL)
```shell
sudo ln -s /usr/local/lib/ollama/rocm/rocblas/library/TensileLibrary_lazy_gfx{1030,1010}.dat

sudoedit /etc/systemd/system/ollama.service
# append to [Service]
Environment="HSA_OVERRIDE_GFX_VERSION=10.1.0"
Environment="OLLAMA_HOST=0.0.0.0"

sudo systemctl daemon-reload
sudo systemctl restart ollama.service
```

PULL AND RUN MODELS (OPTIONAL)
```shell
ollama run deepseek-r1:8b
```

UNINSTALL FROM HOST
```shell
sudo systemctl stop ollama
sudo systemctl disable ollama

sudo rm /usr/local/bin/ollama
sudo rm /usr/local/lib/ollama

sudo rm /etc/systemd/system/ollama.service
sudo systemctl daemon-reload

sudo userdel ollama
sudo groupdel ollama

sudo rm -r /usr/share/ollama

rm -r ~/.ollama
```
