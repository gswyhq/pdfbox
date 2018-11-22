
第一步, 构建镜像：
docker build -t pdfbox-app:2.0.12 -f Dockerfile  .

第二步，使用构建的镜像提取文本：
docker run -v $PWD:/mnt --rm -it pdfbox-app:2.0.12 ExtractText /mnt/test.pdf
