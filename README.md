
构建镜像：
`docker build -t gswyhq/pdfbox -f Dockerfile  . `

使用构建的镜像提取文本：
`docker run -v $PWD:/mnt --rm -it gswyhq/pdfbox ExtractText /mnt/test.pdf`

```
PDFBox version: "2.0.12"
Usage: java -jar pdfbox-app-x.y.z.jar <command> <args..>

PDFBox命令行工具
    Decrypt：  解密一个PDF文档
    Encrypt：  加密一个PDF文档
    ExtractText：从PDF文档中提取字符串
    ExtractImages : 提取图像
    OverlayPDF： 覆盖PDF文件
    PrintPDF ： 打印PDF文件
    PDFDebugger： 列出PDF文档本身的信息
    PDFReader ： 读取PDF文档
    PDFMerger： 合并PDF文档
    PDFSplit : 拆分PDF文档
    PDFToImage： 把PDF文档转换成一张图片
    TextToPDF： 把一段文本转换成一个PDF文件
    WriteDecodedDoc： 解压缩一个PDF文件

# 提取文本
Usage: java -jar pdfbox-app-x.y.z.jar ExtractText [options] <inputfile> [output-text-file]

Options:
  -password  <password>        : Password to decrypt document
  -encoding  <output encoding> : UTF-8 (default) or ISO-8859-1, UTF-16BE, UTF-16LE, etc.
  -console                     : Send text to console instead of file
  -html                        : Output in HTML format instead of raw text
  -sort                        : Sort the text before writing
  -ignoreBeads                 : Disables the separation by beads
  -debug                       : Enables debug output about the time consumption of every stage
  -startPage <number>          : The first page to start extraction(1 based)
  -endPage <number>            : The last page to extract(inclusive)
  <inputfile>                  : The PDF document to use
  [output-text-file]           : The file to write the text to

docker run -v $PWD:/mnt --rm -it gswyhq/pdfbox ExtractText /mnt/test.pdf

# 分割PDF文件
Usage: java -jar pdfbox-app-x.y.z.jar PDFSplit [options] <inputfile>

Options:
  -password  <password>  : Password to decrypt document
  -split     <integer>   : split after this many pages (default 1, if startPage and endPage are unset)
  -startPage <integer>   : start page
  -endPage   <integer>   : end page
  -outputPrefix <prefix> : Filename prefix for splitted files
  <inputfile>            : The PDF document to use

docker run -v $PWD:/mnt --rm -it gswyhq/pdfbox PDFSplit -split 1 -startPage 1 -outputPrefix /mnt/test.pdf
其中 -startPage 1 表示从第一页开始拆分
        -split 1 表示被拆分后，每个单独的被拆分的PDF文件是多少页， 这里是1页一个文件；

# 合并PDF文件
Usage: java -jar pdfbox-app-x.y.z.jar PDFMerger <inputfiles 2..n> <outputfile>

Options:
  <inputfiles 2..n> : 2 or more source PDF documents to merge
  <outputfile>      : The PDF document to save the merged documents to

docker run -v $PWD:/mnt --rm -it gswyhq/pdfbox PDFMerger /mnt/doc1.pdf /mnt/doc2.pdf /mnt/merger.pdf

# 打印PDF文件：
Usage: java -jar pdfbox-app-x.y.z.jar PrintPDF [options] <inputfile>

Options:
  -password  <password>                : Password to decrypt document
  -printerName <name>                  : Print to specific printer
  -orientation auto|portrait|landscape : Print using orientation
                                           (default: auto)
  -border                              : Print with border
  -dpi                                 : Render into intermediate image with
                                           specific dpi and then print
  -silentPrint                         : Print without printer dialog box

# 解压缩PDF文件WriteDecodedDoc
Usage: java -jar pdfbox-app-x.y.z.jar WriteDecodedDoc [options] <inputfile> [outputfile]

Options:
  -password <password> : Password to decrypt the document
  -skipImages          : Don't uncompress images
  <inputfile>          : The PDF document to be decompressed
  [outputfile]         : The filename for the decompressed pdf

# 读取PDF文件(需要图形化界面才可以展示)
java -jar pdfbox-app-2.0.12.jar PDFReader test.pdf

```
