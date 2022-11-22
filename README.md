***SUI TEŞVİKLİ TESTNET REHBERİ***

Sui testnetine katılmak için seçildiyseniz aşağıdaki kılavuzdan full-node kurabilirsiniz.

![image](https://user-images.githubusercontent.com/105454859/203421284-59e8efda-9cb6-4500-96f7-612f4da50a49.png)

Sadece seçilen kullanıcılar ödül alabilecekler!

**Minimum Sistem Gereksinimleri**

CPUs: 10 core
RAM: 32 GB
Storage: 1 TB

**Sui Testnette full-node kurmak için iki yöntem var:**

1- Açık Kaynak kullanarak verileri çekmek ve node'u çalıştırmak
2- Docker yazılımı kullanarak node'u çalıştırmak.
Biz docker kullanarak node'umuzu kuracağımız bir rehber oluşturduk, docker kullanarak yapmanız gerekenler aşağıdaki gibidir:

**1. Linux gereksinimlerini yüklemek.**

 sudo apt update \ && apt-get install -y --no-install-recommends \apt-transport-https \ca-certificates \curl \software-properties-common

**2. Docker kurmak**

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

sudo apt update

sudo apt install docker-ce

**3. Kullanıcı adınızı Docker grubunun içerisine eklemek.**

sudo usermod -aG docker {USER}

#User adınızı öğrenmek için echo $USER yazın.

**4. Docker Compose indirin.**

sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version

**5.SUI Directory Oluşturun.**

mkdir -p $HOME/sui

cd $HOME/sui

**6. Fullnode.yaml dosyasını indirin.**

wget -O $HOME/sui/fullnode-template.yaml https://github.com/MystenLabs/sui/raw/main/crates/sui-config/data/fullnode-template.yaml

**7. Genesis state dosyasını indirin.**

cd $HOME/.sui

wget https://raw.githubusercontent.com/SuiExternal/sui-external/main/genesis.blob

**8. Gerekli docker-compose dosyasını indirin ve Sui görselini güncelleyin.**

IMAGE="mysten/sui-node:99b4e7ca83b6d1abe312f5afc04840dce331238b"

wget -O $HOME/sui/docker-compose.yaml https://raw.githubusercontent.com/MystenLabs/sui/main/docker/fullnode/docker-compose.yaml

sed -i.bak "s|image:.*|image: $IMAGE|" $HOME/sui/docker-compose.yaml

**9. Docker container içindeki Sui full-node'u çalıştırın.**

docker-compose up -d --force-recreate

**10. Container içindeki logları inceleyin.**

docker ps

#Docker ps komutundan sonra container id'de yazan numarayı kopyalayın

docker logs -f <container id>

 #Kopyaladığınız id yi <container id> yi silerek yapıştırın ve logları inceleyin.
  
 **Yardımcı Kodlar**
  
**1. Güncelleme gerektiğinde**
  
  docker-compose down --volumes
  
**2. Node'u yeniden çalıştırmak için**
  
  docker-compose up -d
  
**Node sync durumunu kontrol etmek için:**
  
  https://www.scale3labs.com/check/sui/testnet

  



