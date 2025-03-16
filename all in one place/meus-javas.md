# Para listar as versões 

- ls /usr/lib/jvm/

---

# Para disponibilizar eles como opções

- sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-11.0.26-oracle-x64/bin/java 1
- sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-17.0.14-oracle-x64/bin/java 2
- sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-21.0.6-oracle-x64/bin/java 3

---

# Para adicionar o compilador 

- sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-11.0.26-oracle-x64/bin/javac 1
- sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-17.0.14-oracle-x64/bin/javac 2
- sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-21.0.6-oracle-x64/bin/javac 3

---

# para escolher as versões
- sudo update-alternatives --config java
- sudo update-alternatives --config javac

---

# Para ver qual versão está usando atualmente

- java -version
- javac -version