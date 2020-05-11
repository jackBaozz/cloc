<a name="___top"></a>
# cloc
*Count Lines of Code*

* * *
cloc counts blank lines, comment lines, and physical lines of source code in many programming languages.

Latest release:  v1.84 (September 22, 2019)

cloc moved to GitHub in September 2015 after being hosted
at http://cloc.sourceforge.net/ since August 2006.

*   [Quick Start](#quick-start-)
*   [Overview](#overview-)
*   [Download](https://github.com/AlDanial/cloc/releases/latest)
    *   [Install via package manager](#install-via-package-manager)
    *   [Stable release](#stable-release)
    *   [Development version](#development-version)
*   [License](#license-)
*   [Why Use cloc?](#why-use-cloc-)
*   [Other Counters](#other-counters-)
*   [Building a Windows Executable](#building-a-windows-executable-)
*   [Basic Use](#basic-use-)
*   [Options](#options-)
*   [Recognized Languages](#recognized-languages-)
*   [How it Works](#how-it-works-)
*   [Advanced Use](#advanced-use-)
    *   [Remove Comments from Source Code](#remove-comments-from-source-code-)
    *   [Work with Compressed Archives](#work-with-compressed-archives-)
    *   [Differences](#differences-)
    *   [Create Custom Language Definitions](#create-custom-language-definitions-)
    *   [Combine Reports](#combine-reports-)
    *   [SQL](#sql-)
    *   [Custom Column Output](#custom-column-output-)
    *   [Wrapping cloc in other scripts](#wrapping-cloc-in-other-scripts-)
    *   [git and UTF8 pathnames](#git-and-UTF8-pathnames-)
    *   [Third Generation Language Scale Factors](#third-generation-language-scale-factors-)
*   [Complex regular subexpression recursion limit ](#complex-regular-subexpression-recursion-limit-)
*   [Limitations](#limitations-)
*   [Requesting Support for Additional Languages](#requesting-support-for-additional-languages-)
*   [Reporting Problems](#reporting-problems-)
*   [Acknowledgments](#acknowledgments-)
*   [Copyright](#copyright-)

<a name="Quick_Start"></a>      []({{{1)
# [Quick Start &#9650;](#___top "click to go to top of document")

Step 1:  Download cloc (several methods, see below) or run cloc's 
[docker image](#Docker-1).  The Windows executable has no requirements.
The source version of cloc requires a Perl interpreter, and the
Docker version of cloc requires a Docker installation.
````
下载cloc（几种方法，见下文）或运行cloc的 
[docker image](#Docker-)。 Windows的可执行文件没有任何要求。
cloc的源代码版本需要一个Perl解释器，而Docker版本的cloc需要安装Docker。
````

Step 2:  Open a terminal (`cmd.exe` on Windows).

Step 3:  Invoke cloc to count your source files, directories, archives,
or git commits.
The executable name differs depending on whether you use the
development source version (`cloc`), source for a
released version (`cloc-1.82.pl`) or a Windows executable
(`cloc-1.82.exe`).  On this page, `cloc` is the generic term
used to refer to any of these.
````
调用cloc来统计你的源文件、目录、存档或 git 提交。
可执行的名称不同，这取决于你是否使用开发源码版本cloc、源码为一个发布的版本 cloc-1.82.pl 或 Windows的可执行文件cloc-1.82.exe。 
本页中的 cloc是通用术语。用于指代其中的任何一个。
````

** 一个文件 **
<pre>
prompt> cloc hello.c
       1 text file.
       1 unique file.
       0 files ignored.

https://github.com/AlDanial/cloc v 1.65  T=0.04 s (28.3 files/s, 340.0 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
C                                1              0              7              5
-------------------------------------------------------------------------------
</pre>

** 一个目录 **
<pre>
prompt> cloc gcc-5.2.0/gcc/c
      16 text files.
      15 unique files.
       3 files ignored.

https://github.com/AlDanial/cloc v 1.65  T=0.23 s (57.1 files/s, 188914.0 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
C                               10           4680           6621          30812
C/C++ Header                     3             99            286            496
-------------------------------------------------------------------------------
SUM:                            13           4779           6907          31308
-------------------------------------------------------------------------------
</pre>

** 档案馆 **

We'll pull cloc's source zip file from GitHub, then count the contents:
<pre>
prompt> wget https://github.com/AlDanial/cloc/archive/master.zip

prompt> cloc master.zip
https://github.com/AlDanial/cloc v 1.65  T=0.07 s (26.8 files/s, 141370.3 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Perl                             2            725           1103           8713
-------------------------------------------------------------------------------
SUM:                             2            725           1103           8713
-------------------------------------------------------------------------------
</pre>

** 一个git仓库，使用一个特定的提交 **

This example uses code from
<a href=https://pypi.python.org/pypi/pudb>PuDB</a>, a fantastic Python debugger.

<pre>
prompt> git clone http://git.tiker.net/trees/pudb.git

prompt> cd pudb

prompt> cloc 6be804e07a5db
      48 text files.
      48 unique files.
      15 files ignored.

github.com/AlDanial/cloc v 1.73  T=0.15 s (223.1 files/s, 46159.0 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Python                          28           1519            728           4659
YAML                             2              9              2             75
Bourne Shell                     3              6              0             17
make                             1              4              6             10
-------------------------------------------------------------------------------
SUM:                            34           1538            736           4761
-------------------------------------------------------------------------------

</pre>

** 特定目录的每个子目录 **

假设你有一个目录，里面有三个不同的git管理的项目，Project0、Project1和Project2。你可以使用你的shell的循环功能来计算每个项目中的代码。
This example uses bash:
<pre>
prompt> for d in ./*/ ; do (cd "$d" && echo "$d" && cloc --vcs git); done
./Project0/
7 text files.
       7 unique files.
       1 file ignored.

github.com/AlDanial/cloc v 1.71  T=0.02 s (390.2 files/s, 25687.6 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
D                                4             61             32            251
Markdown                         1              9              0             38
make                             1              0              0              4
-------------------------------------------------------------------------------
SUM:                             6             70             32            293
-------------------------------------------------------------------------------
./Project1/
       7 text files.
       7 unique files.
       0 files ignored.

github.com/AlDanial/cloc v 1.71  T=0.02 s (293.0 files/s, 52107.1 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Go                               7            165            282            798
-------------------------------------------------------------------------------
SUM:                             7            165            282            798
-------------------------------------------------------------------------------
./Project2/
      49 text files.
      47 unique files.
      13 files ignored.

github.com/AlDanial/cloc v 1.71  T=0.10 s (399.5 files/s, 70409.4 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Python                          33           1226           1026           3017
C                                4            327            337            888
Markdown                         1             11              0             28
YAML                             1              0              2             12
-------------------------------------------------------------------------------
SUM:                            39           1564           1365           3945
-------------------------------------------------------------------------------
</pre>

[](1}}})
<a name="Overview"></a>      []({{{1)
# [综述 &#9650;](#___top "click to go to top of document")

Translations:
[Arabic](http://www.garciniacambogiareviews.ca/translations/aldanial-cloc/),
[Armenian](http://students.studybay.com/?p=34),
[Belarussian](http://www.besteonderdelen.nl/blog/?p=5426),
[Bulgarian](http://www.ajoft.com/wpaper/aj-cloc.html),
[Hungarian](http://www.forallworld.com/cloc-grof-sornyi-kodot/),
[]( [Polish](http://www.trevister.com/blog/cloc.html), )
[]( [Russian](http://someblogscience.com/cloc.html), )
[Portuguese](https://www.homeyou.com/~edu/cloc),
[Serbo-Croatian](http://science.webhostinggeeks.com/cloc),
[Romanian](http://www.bildelestore.dk/blog/cloc-contele-de-linii-de-cod/),
[Slovakian](http://newknowledgez.com/cloc.html),
[Tamil](http://healthcareadministrationdegree.co/socialwork/aldanial-cloc/)
[]( [Ukrainian](http://blog.kudoybook.com/cloc/) )

cloc counts blank lines, comment lines, and physical lines of source
code in [many programming languages](#Languages). Given two versions of
a code base, cloc can compute differences in blank, comment, and source
lines. It is written entirely in Perl with no dependencies outside the
standard distribution of Perl v5.6 and higher (code from some external
modules is [embedded within
cloc](https://github.com/AlDanial/cloc#regexp_common)) and so is
quite portable. cloc is known to run on many flavors of Linux, FreeBSD,
NetBSD, OpenBSD, Mac OS X, AIX, HP-UX, Solaris, IRIX, z/OS, and Windows.
(To run the Perl source version of cloc on Windows one needs
[ActiveState Perl](http://www.activestate.com/activeperl) 5.6.1 or
higher, [Strawberry Perl](http://strawberryperl.com/),
[Cygwin](http://www.cygwin.com/),
[MobaXTerm](http://mobaxterm.mobatek.net/) with the Perl plug-in
installed,
or
a mingw environment and terminal such as provided by
[Git for Windows](https://gitforwindows.org/).
Alternatively one can use the Windows binary of cloc
generated with [PAR::Packer](http://search.cpan.org/~rschupp/PAR-Packer-1.019/lib/pp.pm)
to run on Windows computers that have neither Perl nor Cygwin.)

cloc contains code from David Wheeler's
[SLOCCount](http://www.dwheeler.com/sloccount/),
Damian Conway and Abigail's Perl module
[Regexp::Common](http://search.cpan.org/%7Eabigail/Regexp-Common-2.120/lib/Regexp/Common.pm),
Sean M. Burke's Perl module
[Win32::Autoglob](http://search.cpan.org/%7Esburke/Win32-Autoglob-1.01/Autoglob.pm),
and Tye McQueen's Perl module
[Algorithm::Diff](http://search.cpan.org/%7Etyemq/Algorithm-Diff-1.1902/lib/Algorithm/Diff.pm).
Language scale factors were derived from Mayes Consulting, LLC web site
http://softwareestimator.com/IndustryData2.htm.
[](1}}})

<a name="Docker"></a> []({{{1)
## 通过docker运行
```shell
docker run --rm -v $PWD:/tmp aldanial/cloc
```
## 通过软件包管理器安装
根据你的操作系统，这些安装方法中的一种可能对你有用（除了Windows的最后两个项目外，其他所有的项目都需要Perl解释器）:

    npm install -g cloc                    # https://www.npmjs.com/package/cloc
    sudo apt install cloc                  # Debian, Ubuntu
    sudo yum install cloc                  # Red Hat, Fedora
    sudo dnf install cloc                  # Fedora 22 or later
    sudo pacman -S cloc                    # Arch
    sudo emerge -av dev-util/cloc          # Gentoo https://packages.gentoo.org/packages/dev-util/cloc
    sudo apk add cloc                      # Alpine Linux
    sudo pkg install cloc                  # FreeBSD
    sudo port install cloc                 # Mac OS X with MacPorts
    brew install cloc                      # Mac OS X with Homebrew
    choco install cloc                     # Windows with Chocolatey
    scoop install cloc                     # Windows with Scoop

**Note**: 我不控制这些软件包。如果你在使用上述软件包中遇到cloc的bug，请在提交问题报告之前，先用github上的最新稳定版的cloc来尝试（链接如下）。
[](1}}})
<a name="Stable"></a> []({{{1)
## 稳定版
https://github.com/AlDanial/cloc/releases/latest

<a name="Dev"></a>
## 开发版
https://github.com/AlDanial/cloc/raw/master/cloc
[](1}}})
<a name="License"></a> []({{{1)
# [License &#9650;](#___top "click to go to top of document")

cloc is licensed under the
[GNU General Public License, v 2](http://www.gnu.org/licenses/gpl-2.0.html),
excluding portions which
are copied from other sources. Code
copied from the Regexp::Common, Win32::Autoglob, and Algorithm::Diff
Perl modules is subject to the
[Artistic License](http://www.opensource.org/licenses/artistic-license-2.0.php).
[](1}}})
<a name="why_use"></a> []({{{1)
# [Why Use cloc? &#9650;](#___top "click to go to top of document")

cloc有许多功能，使其易于使用、彻底、可扩展和便携:

1.  以一个独立的文件形式存在，只需下载文件并运行即可。
2.  可以从文件中读取语言注释定义，从而有可能使用还不存在的计算机语言。
3.  允许按语言和项目对多个运行结果进行汇总。
4.  可以产生多种格式的结果。纯文本、SQL、JSON、JSON、XML、YAML、逗号分隔值。
5.  可以对压缩后的压缩文件（tar balls, Zip files, Java .ear files）中的代码进行统计。
6.  具有众多的故障排除选项。
7.  处理带空格和其他不正常字符的文件和目录名。
8.  没有标准的Perl发行版之外的依赖性。
9.  可以在 Linux, FreeBSD, NetBSD, OpenBSD, Mac OS X, AIX, HP-UX, Solaris, IRIX, 和 z/OS 系统上运行，并支持 Perl 5.6 或更高版本。源版本可以在Windows上运行，可以使用ActiveState Perl、Strawberry Perl、Cygwin或MobaXTerm+Perl插件。也可以在Windows系统上运行Windows二进制，它没有任何依赖性。

[](1}}})

<a name="Other_Counters"></a> []({{{1)
# [Other Counters &#9650;](#___top "click to go to top of document")

如果cloc不适合你的需求，这里有其他免费的计数器可以考虑:

*   [loc](https://github.com/cgag/loc/)
*   [gocloc](https://github.com/hhatto/gocloc/)
*   [Ohcount](https://github.com/blackducksoftware/ohcount/)
*   [scc](https://github.com/boyter/scc/)
*   [sclc](https://code.google.com/archive/p/sclc/)
*   [SLOCCount](http://www.dwheeler.com/sloccount/)
*   [Sonar](http://www.sonarsource.org/)
*   [tokei](https://github.com/Aaronepower/tokei/)
*   [Unified Code Count](http://csse.usc.edu/ucc_new/wordpress/)

其他参考资料:

*   QSM's [directory](http://www.qsm.com/CodeCounters.html) of code counting tools.
*   The [Wikipedia entry](http://en.wikipedia.org/wiki/Source_lines_of_code) for source code line counts.
[](1}}})

# <a name="regexp_common">Regexp::Common, Digest::MD5, Win32::Autoglob, Algorithm::Diff</a> []({{{1)

Although cloc does not need Perl modules outside those found in the
standard distribution, cloc does rely on a few external modules. Code
from three of these external modules--Regexp::Common, Win32::Autoglob,
and Algorithm::Diff--is embedded within cloc. A fourth module,
Digest::MD5, is used only if it is available. If cloc finds
Regexp::Common or Algorithm::Diff installed locally it will use those
installation. If it doesn't, cloc will install the parts of
Regexp::Common and/or Algorithm:Diff it needs to temporary directories
that are created at the start of a cloc run then removed when the run is
complete. The necessary code from Regexp::Common v2.120 and
Algorithm::Diff v1.1902 are embedded within the cloc source code (see
subroutines `Install_Regexp_Common()` and `Install_Algorithm_Diff()` ).
Only three lines are needed from Win32::Autoglob and these are included
directly in cloc.

Additionally, cloc will use Digest::MD5 to validate uniqueness among
equally-sized input files if Digest::MD5 is installed locally.

A parallel processing option, <tt>--processes=<i>N</i></tt>, was introduced with
cloc version 1.76 to enable faster runs on multicored machines.  However,
to use it, one must have the module Parallel::ForkManager installed.
This module does not work reliably on Windows so parallel processing
will only work on Unix-like operating systems.

The Windows binary is built on a computer that has both Regexp::Common
and Digest::MD5 installed locally.
[](1}}})
<a name="building_exe"></a> []({{{1)
# [构建一个Windows可执行文件 &#9650;](#___top "click to go to top of document")

The Windows downloads
<tt>cloc-1.70.exe</tt> and
<tt>cloc-1.72.exe</tt> were
built with [PAR::Packer](http://search.cpan.org/~rschupp/PAR-Packer-1.019/lib/pp.pm)
and Strawberry Perl 5.24.0.1
on an Amazon Web Services t2.micro instance running Microsoft Windows Server 2008
(32 bit for 1.70 and 1.72; 64 bit for 1.74).

Releases 1.74 through 1.84
were was built on a 32 bit Windows 7 virtual machine (IE11.Win7.For.Windows.VirtualBox.zip
pulled from https://developer.microsoft.com/en-us/microsoft-edge/tools/vms/)
using Strawberry Perl 5.26.1.1.

The <tt>cloc-1.66.exe</tt> executable was built with [PAR::Packer](http://search.cpan.org/~rschupp/PAR-Packer-1.019/lib/pp.pm)
on a 32 bit Windows 7 VirtualBox image
pulled from https://dev.windows.com/en-us/microsoft-edge/tools/vms/linux/
and running on an Ubuntu 15.10 host.
The virtual machine ran
[Strawberry Perl](http://strawberryperl.com/) version 5.22.1.
Windows executables of cloc versions
1.60 and earlier were built with
[perl2exe](http://www.indigostar.com/perl2exe.htm) on a 32 bit Windows
XP computer. A small modification was made to the cloc source code
before passing it to perl2exe; lines 87 and 88 were uncommented:

<pre>
<font color="gray">85</font>  # Uncomment next two lines when building Windows executable with perl2exe
<font color="gray">86</font>  # or if running on a system that already has Regexp::Common.
<font color="gray">87</font>  <font color="red">#use Regexp::Common;</font>
<font color="gray">88</font>  <font color="red">#$HAVE_Rexexp_Common = 1;</font>
</pre>

#### Windows的可执行文件可以安全运行吗？ 它是否有恶意软件？

理想情况下，没有人需要Windows可执行文件，因为他们的机器上安装了Perl解释器，可以运行cloc源文件。
但是，在集中管理的企业Windows机器上，这可能会有困难或不可能。

随 cloc 一起分发的 Windows 可执行文件是作为无病毒和无恶意软件的".exe "的最佳努力提供的。
我们鼓励您针对该可执行程序运行自己的病毒扫描器，并检查网站https://www.virustotal.com/ .
最近版本的条目是:

cloc-1.84.exe:
https://www.virustotal.com/gui/file/e73d490c1e4ae2f50ee174005614029b4fa2610dcb76988714839d7be68479af/detection

cloc-1.82.exe:
https://www.virustotal.com/#/file/2e5fb443fdefd776d7b6b136a25e5ee2048991e735042897dbd0bf92efb16563/detection

cloc-1.80.exe:
https://www.virustotal.com/#/file/9e547b01c946aa818ffad43b9ebaf05d3da08ed6ca876ef2b6847be3bf1cf8be/detection

cloc-1.78.exe:
https://www.virustotal.com/#/file/256ade3df82fa92febf2553853ed1106d96c604794606e86efd00d55664dd44f/detection

cloc-1.76.exe:
https://www.virustotal.com/#/url/c1b9b9fe909f91429f95d41e9a9928ab7c58b21351b3acd4249def2a61acd39d/detection

cloc-1.74_x86.exe:
https://www.virustotal.com/#/file/b73dece71f6d3199d90d55db53a588e1393c8dbf84231a7e1be2ce3c5a0ec75b/detection

cloc 1.72 exe:
https://www.virustotal.com/en/url/8fd2af5cd972f648d7a2d7917bc202492012484c3a6f0b48c8fd60a8d395c98c/analysis/

cloc 1.70 exe:
https://www.virustotal.com/en/url/63edef209099a93aa0be1a220dc7c4c7ed045064d801e6d5daa84ee624fc0b4a/analysis/

cloc 1.68 exe:
https://www.virustotal.com/en/file/c484fc58615fc3b0d5569b9063ec1532980281c3155e4a19099b11ef1c24443b/analysis/

cloc 1.66 exe:
https://www.virustotal.com/en/file/54d6662e59b04be793dd10fa5e5edf7747cf0c0cc32f71eb67a3cf8e7a171d81/analysis/1453601367/

#### 为什么Windows的可执行程序这么大?

Windows executables of cloc versions 1.60 and earlier, created with
perl2exe as noted above, are about 1.6 MB, while versions 1.62 and 1.54, created
with `PAR::Packer`, are 11 MB.

Version 1.66, built with a newer version of `PAR::Packer`, is about 5.5 MB.
Why are the `PAR::Packer`, executables so
much larger than those built with perl2exe? My theory is that perl2exe
uses smarter tree pruning logic
than `PAR::Packer`, but that's pure speculation.

#### 创建你自己的可执行文件
The most robust option for creating a Windows executable of
cloc is to use [ActiveState's Perl Development Kit](http://www.activestate.com/perl-dev-kit).
It includes a utility, `perlapp`, which can build stand-alone
Windows, Mac, and Linux binaries of Perl source code.

[perl2exe](http://www.indigostar.com/perl2exe.php)
will also do the trick.  If you do have `perl2exe`, modify lines
84-87 in the cloc source code for a minor code
modification that is necessary to make a cloc Windows executable.

Otherwise, to build a Windows executable with `pp` from
`PAR::Packer`, first install a Windows-based Perl distribution
(for example Strawberry Perl or ActivePerl) following their
instructions. Next, open a command prompt, aka a DOS window and install
the PAR::Packer module. Finally, invoke the newly installed `pp`
command with the cloc source code to create an `.exe` file:

<pre>
C:> cpan -i Digest::MD5
C:> cpan -i Regexp::Common
C:> cpan -i Algorithm::Diff
C:> cpan -i PAR::Packer
C:> pp -M Digest::MD5 -c -x -o cloc-1.84.exe cloc-1.84.pl
</pre>

A variation on the instructions above is if you installed the portable
version of Strawberry Perl, you will need to run `portableshell.bat` first
to properly set up your environment.

[](1}}})
<a name="Basic_Use"></a> []({{{1)
# [基本用途 &#9650;](#___top "click to go to top of document")

cloc 是一个命令行程序，它以文件、目录和/或存档名作为输入。下面是一个在 Perl v5.22.0 源码发行版中运行 cloc 的例子。

<pre>
prompt> cloc perl-5.22.0.tar.gz
    5605 text files.
    5386 unique files.
    2176 files ignored.

https://github.com/AlDanial/cloc v 1.65  T=25.49 s (134.7 files/s, 51980.3 lines/s)
-----------------------------------------------------------------------------------
Language                         files          blank        comment           code
-----------------------------------------------------------------------------------
Perl                              2892         136396         184362         536445
C                                  130          24676          33684         155648
C/C++ Header                       148           9766          16569         147858
Bourne Shell                       112           4044           6796          42668
Pascal                               8            458           1603           8592
XML                                 33            142              0           2410
YAML                                49             20             15           2078
C++                                 10            313            277           2033
make                                 4            426            488           1986
Prolog                              12            438              2           1146
JSON                                14              1              0           1037
yacc                                 1             85             76            998
Windows Message File                 1            102             11            489
DOS Batch                           14             92             41            389
Windows Resource File                3             10              0             85
D                                    1              5              7              8
Lisp                                 2              0              3              4
-----------------------------------------------------------------------------------
SUM:                              3434         176974         243934         903874
-----------------------------------------------------------------------------------

</pre>

要在Windows电脑上运行cloc，首先必须打开一个命令(又名DOS)窗口，从命令行中调用cloc.exe .
[](1}}})
<a name="Options"></a> []({{{1)
# [选项 &#9650;](#___top "click to go to top of document")

<pre>
prompt> cloc --help

Usage: cloc [options] &lt;file(s)/dir(s)/git hash(es)&gt; | &lt;set 1&gt; &lt;set 2&gt; | &lt;report files&gt;

 Count, or compute differences of, physical lines of source code in the
 given files (may be archives such as compressed tarballs or zip files,
 or git commit hashes or branch names) and/or recursively below the
 given directories.

 Input Options
   --extract-with=&lt;cmd&gt;      This option is only needed if cloc is unable
                             to figure out how to extract the contents of
                             the input file(s) by itself.
                             Use &lt;cmd&gt; to extract binary archive files (e.g.:
                             .tar.gz, .zip, .Z).  Use the literal '&gt;FILE&lt;' as
                             a stand-in for the actual file(s) to be
                             extracted.  For example, to count lines of code
                             in the input files
                                gcc-4.2.tar.gz  perl-5.8.8.tar.gz
                             on Unix use
                               --extract-with='gzip -dc &gt;FILE&lt; | tar xf -'
                             or, if you have GNU tar,
                               --extract-with='tar zxf &gt;FILE&lt;'
                             and on Windows use, for example:
                               --extract-with="\"c:\Program Files\WinZip\WinZip32.exe\" -e -o &gt;FILE&lt; ."
                             (if WinZip is installed there).
   --list-file=&lt;file&gt;        Take the list of file and/or directory names to
                             process from &lt;file&gt;, which has one file/directory
                             name per line.  Only exact matches are counted;
                             relative path names will be resolved starting from
                             the directory where cloc is invoked.
                             See also --exclude-list-file.
   --vcs=&lt;VCS&gt;               Invoke a system call to &lt;VCS&gt; to obtain a list of
                             files to work on.  If &lt;VCS&gt; is 'git', then will
                             invoke 'git ls-files' to get a file list and
                             'git submodule status' to get a list of submodules
                             whose contents will be ignored.  See also --git
                             which accepts git commit hashes and branch names.
                             If &lt;VCS&gt; is 'svn' then will invoke 'svn list -R'.
                             The primary benefit is that cloc will then skip
                             files explicitly excluded by the versioning tool
                             in question, ie, those in .gitignore or have the
                             svn:ignore property.
                             Alternatively &lt;VCS&gt; may be any system command
                             that generates a list of files.
                             Note:  cloc must be in a directory which can read
                             the files as they are returned by &lt;VCS&gt;.  cloc will
                             not download files from remote repositories.
                             'svn list -R' may refer to a remote repository
                             to obtain file names (and therefore may require
                             authentication to the remote repository), but
                             the files themselves must be local.
   --unicode                 Check binary files to see if they contain Unicode
                             expanded ASCII text.  This causes performance to
                             drop noticeably.

 Processing Options
   --autoconf                Count .in files (as processed by GNU autoconf) of
                             recognized languages.  See also --no-autogen.
   --by-file                 Report results for every source file encountered.
   --by-file-by-lang         Report results for every source file encountered
                             in addition to reporting by language.
   --config &lt;file&gt;           Read command line switches from &lt;file&gt; instead of
                             the default location of /home/al/.config/cloc/options.txt.
                             The file should contain one switch, along with
                             arguments (if any), per line.  Blank lines and lines
                             beginning with '#' are skipped.  Options given on
                             the command line take priority over entries read from
                             the file.
   --count-and-diff &lt;set1&gt; &lt;set2&gt;
                             First perform direct code counts of source file(s)
                             of &lt;set1&gt; and &lt;set2&gt; separately, then perform a diff
                             of these.  Inputs may be pairs of files, directories,
                             or archives.  If --out or --report-file is given,
                             three output files will be created, one for each
                             of the two counts and one for the diff.  See also
                             --diff, --diff-alignment, --diff-timeout,
                             --ignore-case, --ignore-whitespace.
   --diff &lt;set1&gt; &lt;set2&gt;      Compute differences in code and comments between
                             source file(s) of &lt;set1&gt; and &lt;set2&gt;.  The inputs
                             may be any mix of files, directories, archives,
                             or git commit hashes.  Use --diff-alignment to
                             generate a list showing which file pairs where
                             compared.  See also --count-and-diff, --diff-alignment,
                             --diff-timeout, --ignore-case, --ignore-whitespace.
   --diff-timeout &lt;N&gt;        Ignore files which take more than &lt;N&gt; seconds
                             to process.  Default is 10 seconds.  Setting &lt;N&gt;
                             to 0 allows unlimited time.  (Large files with many
                             repeated lines can cause Algorithm::Diff::sdiff()
                             to take hours.)
   --follow-links            [Unix only] Follow symbolic links to directories
                             (sym links to files are always followed).
   --force-lang=&lt;lang&gt;[,&lt;ext&gt;]
                             Process all files that have a &lt;ext&gt; extension
                             with the counter for language &lt;lang&gt;.  For
                             example, to count all .f files with the
                             Fortran 90 counter (which expects files to
                             end with .f90) instead of the default Fortran 77
                             counter, use
                               --force-lang="Fortran 90",f
                             If &lt;ext&gt; is omitted, every file will be counted
                             with the &lt;lang&gt; counter.  This option can be
                             specified multiple times (but that is only
                             useful when &lt;ext&gt; is given each time).
                             See also --script-lang, --lang-no-ext.
   --force-lang-def=&lt;file&gt;   Load language processing filters from &lt;file&gt;,
                             then use these filters instead of the built-in
                             filters.  Note:  languages which map to the same
                             file extension (for example:
                             MATLAB/Mathematica/Objective C/MUMPS/Mercury;
                             Pascal/PHP; Lisp/OpenCL; Lisp/Julia; Perl/Prolog)
                             will be ignored as these require additional
                             processing that is not expressed in language
                             definition files.  Use --read-lang-def to define
                             new language filters without replacing built-in
                             filters (see also --write-lang-def,
                             --write-lang-def-incl-dup).
   --git                     Forces the inputs to be interpreted as git targets
                             (commit hashes, branch names, et cetera) if these
                             are not first identified as file or directory
                             names.  This option overrides the --vcs=git logic
                             if this is given; in other words, --git gets its
                             list of files to work on directly from git using
                             the hash or branch name rather than from
                             'git ls-files'.  This option can be used with
                             --diff to perform line count diffs between git
                             commits, or between a git commit and a file,
                             directory, or archive.  Use -v/--verbose to see
                             the git system commands cloc issues.
   --ignore-whitespace       Ignore horizontal white space when comparing files
                             with --diff.  See also --ignore-case.
   --ignore-case             Ignore changes in case; consider upper- and lower-
                             case letters equivalent when comparing files with
                             --diff.  See also --ignore-whitespace.
   --lang-no-ext=&lt;lang&gt;      Count files without extensions using the &lt;lang&gt;
                             counter.  This option overrides internal logic
                             for files without extensions (where such files
                             are checked against known scripting languages
                             by examining the first line for #!).  See also
                             --force-lang, --script-lang.
   --max-file-size=&lt;MB&gt;      Skip files larger than &lt;MB&gt; megabytes when
                             traversing directories.  By default, &lt;MB&gt;=100.
                             cloc's memory requirement is roughly twenty times
                             larger than the largest file so running with
                             files larger than 100 MB on a computer with less
                             than 2 GB of memory will cause problems.
                             Note:  this check does not apply to files
                             explicitly passed as command line arguments.
   --no-autogen[=list]       Ignore files generated by code-production systems
                             such as GNU autoconf.  To see a list of these files
                             (then exit), run with --no-autogen list
                             See also --autoconf.
   --original-dir            [Only effective in combination with
                             --strip-comments]  Write the stripped files
                             to the same directory as the original files.
   --read-binary-files       Process binary files in addition to text files.
                             This is usually a bad idea and should only be
                             attempted with text files that have embedded
                             binary data.
   --read-lang-def=&lt;file&gt;    Load new language processing filters from &lt;file&gt;
                             and merge them with those already known to cloc.
                             If &lt;file&gt; defines a language cloc already knows
                             about, cloc's definition will take precedence.
                             Use --force-lang-def to over-ride cloc's
                             definitions (see also --write-lang-def,
                             --write-lang-def-incl-dup).
   --script-lang=&lt;lang&gt;,&lt;s&gt;  Process all files that invoke &lt;s&gt; as a #!
                             scripting language with the counter for language
                             &lt;lang&gt;.  For example, files that begin with
                                #!/usr/local/bin/perl5.8.8
                             will be counted with the Perl counter by using
                                --script-lang=Perl,perl5.8.8
                             The language name is case insensitive but the
                             name of the script language executable, &lt;s&gt;,
                             must have the right case.  This option can be
                             specified multiple times.  See also --force-lang,
                             --lang-no-ext.
   --sdir=&lt;dir&gt;              Use &lt;dir&gt; as the scratch directory instead of
                             letting File::Temp chose the location.  Files
                             written to this location are not removed at
                             the end of the run (as they are with File::Temp).
   --skip-uniqueness         Skip the file uniqueness check.  This will give
                             a performance boost at the expense of counting
                             files with identical contents multiple times
                             (if such duplicates exist).
   --stdin-name=&lt;file&gt;       Give a file name to use to determine the language
                             for standard input.  (Use - as the input name to
                             receive source code via STDIN.)
   --strip-comments=&lt;ext&gt;    For each file processed, write to the current
                             directory a version of the file which has blank
                             and commented lines removed (in-line comments
                             persist).  The name of each stripped file is the
                             original file name with .&lt;ext&gt; appended to it.
                             It is written to the current directory unless
                             --original-dir is on.
   --strip-str-comments      Replace comment markers embedded in strings with
                             'xx'.  This attempts to work around a limitation
                             in Regexp::Common::Comment where comment markers
                             embedded in strings are seen as actual comment
                             markers and not strings, often resulting in a
                             'Complex regular subexpression recursion limit'
                             warning and incorrect counts.  There are two
                             disadvantages to using this switch:  1/code count
                             performance drops, and 2/code generated with
                             --strip-comments will contain different strings
                             where ever embedded comments are found.
   --sum-reports             Input arguments are report files previously
                             created with the --report-file option.  Makes
                             a cumulative set of results containing the
                             sum of data from the individual report files.
   --processes=NUM           [Available only on systems with a recent version
                             of the Parallel::ForkManager module.  Not
                             available on Windows.] Sets the maximum number of
                             cores that cloc uses.  The default value of 0
                             disables multiprocessing.
   --unix                    Override the operating system autodetection
                             logic and run in UNIX mode.  See also
                             --windows, --show-os.
   --use-sloccount           If SLOCCount is installed, use its compiled
                             executables c_count, java_count, pascal_count,
                             php_count, and xml_count instead of cloc's
                             counters.  SLOCCount's compiled counters are
                             substantially faster than cloc's and may give
                             a performance improvement when counting projects
                             with large files.  However, these cloc-specific
                             features will not be available: --diff,
                             --count-and-diff, --strip-comments, --unicode.
   --windows                 Override the operating system autodetection
                             logic and run in Microsoft Windows mode.
                             See also --unix, --show-os.

 Filter Options
   --exclude-dir=&lt;D1&gt;[,D2,]  Exclude the given comma separated directories
                             D1, D2, D3, et cetera, from being scanned.  For
                             example  --exclude-dir=.cache,test  will skip
                             all files and subdirectories that have /.cache/
                             or /test/ as their parent directory.
                             Directories named .bzr, .cvs, .hg, .git, .svn,
                             and .snapshot are always excluded.
                             This option only works with individual directory
                             names so including file path separators is not
                             allowed.  Use --fullpath and --not-match-d=&lt;regex&gt;
                             to supply a regex matching multiple subdirectories.
   --exclude-ext=&lt;ext1&gt;[,&lt;ext2&gt;[...]]
                             Do not count files having the given file name
                             extensions.
   --exclude-lang=&lt;L1&gt;[,L2[...]]
                             Exclude the given comma separated languages
                             L1, L2, L3, et cetera, from being counted.
   --exclude-list-file=&lt;file&gt;  Ignore files and/or directories whose names
                             appear in &lt;file&gt;.  &lt;file&gt; should have one file
                             name per line.  Only exact matches are ignored;
                             relative path names will be resolved starting from
                             the directory where cloc is invoked.
                             See also --list-file.
   --fullpath                Modifies the behavior of --match-f, --not-match-f,
                             and --not-match-d to include the file's path
                             in the regex, not just the file's basename.
                             (This does not expand each file to include its
                             absolute path, instead it uses as much of
                             the path as is passed in to cloc.)
                             Note:  --match-d always looks at the full
                             path and therefore is unaffected by --fullpath.
   --include-ext=&lt;ext1&gt;[,ext2[...]]
                             Count only languages having the given comma
                             separated file extensions.  Use --show-ext to
                             see the recognized extensions.
   --include-lang=&lt;L1&gt;[,L2[...]]
                             Count only the given comma separated languages
                             L1, L2, L3, et cetera.  Use --show-lang to see
                             the list of recognized languages.
   --match-d=&lt;regex&gt;         Only count files in directories matching the Perl
                             regex.  For example
                               --match-d='/(src|include)/'
                             only counts files in directories containing
                             /src/ or /include/.  Unlike --not-match-d,
                             --match-f, and --not-match-f, --match-d always
                             compares the fully qualified path against the
                             regex.
   --not-match-d=&lt;regex&gt;     Count all files except those in directories
                             matching the Perl regex.  Only the trailing
                             directory name is compared, for example, when
                             counting in /usr/local/lib, only 'lib' is
                             compared to the regex.
                             Add --fullpath to compare parent directories to
                             the regex.
                             Do not include file path separators at the
                             beginning or end of the regex.
   --match-f=&lt;regex&gt;         Only count files whose basenames match the Perl
                             regex.  For example
                               --match-f='^[Ww]idget'
                             only counts files that start with Widget or widget.
                             Add --fullpath to include parent directories
                             in the regex instead of just the basename.
   --not-match-f=&lt;regex&gt;     Count all files except those whose basenames
                             match the Perl regex.  Add --fullpath to include
                             parent directories in the regex instead of just
                             the basename.
   --skip-archive=&lt;regex&gt;    Ignore files that end with the given Perl regular
                             expression.  For example, if given
                               --skip-archive='(zip|tar(.(gz|Z|bz2|xz|7z))?)'
                             the code will skip files that end with .zip,
                             .tar, .tar.gz, .tar.Z, .tar.bz2, .tar.xz, and
                             .tar.7z.
   --skip-win-hidden         On Windows, ignore hidden files.

 Debug Options
   --categorized=&lt;file&gt;      Save names of categorized files to &lt;file&gt;.
   --counted=&lt;file&gt;          Save names of processed source files to &lt;file&gt;.
   --diff-alignment=&lt;file&gt;   Write to &lt;file&gt; a list of files and file pairs
                             showing which files were added, removed, and/or
                             compared during a run with --diff.  This switch
                             forces the --diff mode on.
   --explain=&lt;lang&gt;          Print the filters used to remove comments for
                             language &lt;lang&gt; and exit.  In some cases the
                             filters refer to Perl subroutines rather than
                             regular expressions.  An examination of the
                             source code may be needed for further explanation.
   --help                    Print this usage information and exit.
   --found=&lt;file&gt;            Save names of every file found to &lt;file&gt;.
   --ignored=&lt;file&gt;          Save names of ignored files and the reason they
                             were ignored to &lt;file&gt;.
   --print-filter-stages     Print processed source code before and after
                             each filter is applied.
   --show-ext[=&lt;ext&gt;]        Print information about all known (or just the
                             given) file extensions and exit.
   --show-lang[=&lt;lang&gt;]      Print information about all known (or just the
                             given) languages and exit.
   --show-os                 Print the value of the operating system mode
                             and exit.  See also --unix, --windows.
   -v[=&lt;n&gt;]                  Verbose switch (optional numeric value).
   -verbose[=&lt;n&gt;]            Long form of -v.
   --version                 Print the version of this program and exit.
   --write-lang-def=&lt;file&gt;   Writes to &lt;file&gt; the language processing filters
                             then exits.  Useful as a first step to creating
                             custom language definitions. Note: languages which
                             map to the same file extension will be excluded.
                             (See also --force-lang-def, --read-lang-def).
   --write-lang-def-incl-dup=&lt;file&gt;
                             Same as --write-lang-def, but includes duplicated
                             extensions.  This generates a problematic language
                             definition file because cloc will refuse to use
                             it until duplicates are removed.

 Output Options
   --3                       Print third-generation language output.
                             (This option can cause report summation to fail
                             if some reports were produced with this option
                             while others were produced without it.)
   --by-percent  X           Instead of comment and blank line counts, show
                             these values as percentages based on the value
                             of X in the denominator:
                                X = 'c'   -&gt; # lines of code
                                X = 'cm'  -&gt; # lines of code + comments
                                X = 'cb'  -&gt; # lines of code + blanks
                                X = 'cmb' -&gt; # lines of code + comments + blanks
                             For example, if using method 'c' and your code
                             has twice as many lines of comments as lines
                             of code, the value in the comment column will
                             be 200%.  The code column remains a line count.
   --csv                     Write the results as comma separated values.
   --csv-delimiter=&lt;C&gt;       Use the character &lt;C&gt; as the delimiter for comma
                             separated files instead of ,.  This switch forces --csv to be on.
   --file-encoding=&lt;E&gt;       Write output files using the &lt;E&gt; encoding instead of
                             the default ASCII (&lt;E&gt; = 'UTF-7').  Examples: 'UTF-16',
                             'euc-kr', 'iso-8859-16'.  Known encodings can be
                             printed with
                               perl -MEncode -e 'print join("\n", Encode-&gt;encodings(":all")), "\n"'
   --hide-rate               Do not show line and file processing rates in the
                             output header. This makes output deterministic.
   --json                    Write the results as JavaScript Object Notation
                             (JSON) formatted output.
   --md                      Write the results as Markdown-formatted text.
   --out=&lt;file&gt;              Synonym for --report-file=&lt;file&gt;.
   --progress-rate=&lt;n&gt;       Show progress update after every &lt;n&gt; files are
                             processed (default &lt;n&gt;=100).  Set &lt;n&gt; to 0 to
                             suppress progress output (useful when redirecting
                             output to STDOUT).
   --quiet                   Suppress all information messages except for
                             the final report.
   --report-file=&lt;file&gt;      Write the results to &lt;file&gt; instead of STDOUT.
   --sql=&lt;file&gt;              Write results as SQL create and insert statements
                             which can be read by a database program such as
                             SQLite.  If &lt;file&gt; is -, output is sent to STDOUT.
   --sql-append              Append SQL insert statements to the file specified
                             by --sql and do not generate table creation
                             statements.  Only valid with the --sql option.
   --sql-project=&lt;name&gt;      Use &lt;name&gt; as the project identifier for the
                             current run.  Only valid with the --sql option.
   --sql-style=&lt;style&gt;       Write SQL statements in the given style instead
                             of the default SQLite format.  Styles include
                             'Oracle' and 'Named_Columns'.
   --sum-one                 For plain text reports, show the SUM: output line
                             even if only one input file is processed.
   --xml                     Write the results in XML.
   --xsl=&lt;file&gt;              Reference &lt;file&gt; as an XSL stylesheet within
                             the XML output.  If &lt;file&gt; is 1 (numeric one),
                             writes a default stylesheet, cloc.xsl (or
                             cloc-diff.xsl if --diff is also given).
                             This switch forces --xml on.
   --yaml                    Write the results in YAML.


</pre>
[](1}}})
<a name="Languages"></a> []({{{1)
# [认可的语言 &#9650;](#___top "click to go to top of document")

<pre>
prompt> cloc --show-lang

ABAP                       (abap)
ActionScript               (as)
Ada                        (ada, adb, ads, pad)
ADSO/IDSM                  (adso)
Agda                       (agda, lagda)
AMPLE                      (ample, dofile, startup)
Ant                        (build.xml, build.xml)
ANTLR Grammar              (g, g4)
Apex Class                 (cls)
Apex Trigger               (trigger)
APL                        (apl, apla, aplc, aplf, apli, apln, aplo, dyalog, dyapp, mipage)
Arduino Sketch             (ino, pde)
AsciiDoc                   (adoc, asciidoc)
ASP                        (asa, ashx, asp, axd)
ASP.NET                    (asax, ascx, asmx, aspx, master, sitemap, webinfo)
AspectJ                    (aj)
Assembly                   (a51, asm, nasm, S, s)
AutoHotkey                 (ahk, ahkl)
awk                        (auk, awk, gawk, mawk, nawk)
Blade                      (blade, blade.php)
Bourne Again Shell         (bash)
Bourne Shell               (sh)
BrightScript               (brs)
builder                    (xml.builder)
C                          (c, cats, ec, idc, pgc)
C Shell                    (csh, tcsh)
C#                         (cs)
C++                        (C, c++, cc, CPP, cpp, cxx, h++, inl, ipp, pcc, tcc, tpp)
C/C++ Header               (H, h, hh, hpp, hxx)
CCS                        (ccs)
Chapel                     (chpl)
Clean                      (dcl, icl)
Clojure                    (boot, cl2, clj, cljs.hl, cljscm, cljx, hic, riemann.config)
ClojureC                   (cljc)
ClojureScript              (cljs)
CMake                      (cmake, cmake.in, CMakeLists.txt)
COBOL                      (CBL, cbl, ccp, COB, cob, cobol, cpy)
CoffeeScript               (_coffee, cakefile, cjsx, coffee, iced)
ColdFusion                 (cfm, cfml)
ColdFusion CFScript        (cfc)
Coq                        (v)
Crystal                    (cr)
CSON                       (cson)
CSS                        (css)
Cucumber                   (feature)
CUDA                       (cu, cuh)
Cython                     (pxd, pxi, pyx)
D                          (d)
DAL                        (da)
Dart                       (dart)
DIET                       (dt)
diff                       (diff, patch)
DITA                       (dita)
DOORS Extension Language   (dxl)
DOS Batch                  (BAT, bat, BTM, btm, cmd, CMD)
Drools                     (drl)
DTD                        (dtd)
dtrace                     (d)
ECPP                       (ecpp)
EEx                        (eex)
EJS                        (ejs)
Elixir                     (ex, exs)
Elm                        (elm)
Embedded Crystal           (ecr)
ERB                        (ERB, erb)
Erlang                     (app.src, emakefile, erl, hrl, rebar.config, rebar.config.lock, rebar.lock, xrl, yrl)
Expect                     (exp)
F#                         (fsi, fs, fs)
F# Script                  (fsx)
Fennel                     (fnl)
Fish Shell                 (fish)
Focus                      (focexec)
Forth                      (4th, e4, f83, fb, forth, fpm, fr, frt, ft, fth, rx, fs, f, for)
Fortran 77                 (F, F77, f77, FOR, FTN, ftn, pfo, f, for)
Fortran 90                 (f90, F90)
Fortran 95                 (F95, f95)
Freemarker Template        (ftl)
FXML                       (fxml)
GDScript                   (gd)
Gencat NLS                 (msg)
Glade                      (glade, ui)
GLSL                       (comp, fp, frag, frg, fsh, fshader, geo, geom, glsl, glslv, gshader, tesc, tese, vert, vrx, vsh, vshader)
Go                         (go)
Gradle                     (gradle, gradle.kts)
Grails                     (gsp)
GraphQL                    (gql, graphql, graphqls)
Groovy                     (gant, groovy, grt, gtpl, gvy, jenkinsfile)
Haml                       (haml, haml.deface)
Handlebars                 (handlebars, hbs)
Harbour                    (hb)
Haskell                    (hs, hsc, lhs)
Haxe                       (hx, hxsl)
HCL                        (hcl, nomad, tf, tfvars)
HLSL                       (cg, cginc, fxh, hlsl, hlsli, shader)
Hoon                       (hoon)
HTML                       (htm, html, html.hl, xht)
IDL                        (dlm, idl, pro)
Idris                      (idr)
Igor Pro                   (ipf)
Imba                       (imba)
INI                        (buildozer.spec, ini, lektorproject, prefs)
InstallShield              (ism)
IPL                        (ipl)
Java                       (java)
JavaScript                 (_js, bones, es6, jake, jakefile, js, jsb, jscad, jsfl, jsm, jss, mjs, njs, pac, sjs, ssjs, xsjs, xsjslib)
JavaServer Faces           (jsf)
JCL                        (jcl)
JSON                       (arcconfig, avsc, composer.lock, geojson, gltf, har, htmlhintrc, json, json-tmlanguage, jsonl, mcmeta, mcmod.info, tern-config, tern-project, tfstate, tfstate.backup, topojson, watchmanconfig, webapp, webmanifest, yyp)
JSON5                      (json5)
JSP                        (jsp, jspf)
JSX                        (jsx)
Julia                      (jl)
Jupyter Notebook           (ipynb)
Kermit                     (ksc)
Korn Shell                 (ksh)
Kotlin                     (kt, ktm, kts)
Lean                       (hlean, lean)
LESS                       (less)
lex                        (l, lex)
LFE                        (lfe)
liquid                     (liquid)
Lisp                       (asd, el, lisp, lsp, cl, jl)
Literate Idris             (lidr)
LiveLink OScript           (oscript)
Logtalk                    (lgt, logtalk)
Lua                        (lua, nse, p8, pd_lua, rbxs, wlua)
m4                         (ac, m4)
make                       (am, gnumakefile, Gnumakefile, Makefile, makefile, mk)
Mako                       (mako, mao)
Markdown                   (contents.lr, markdown, md, mdown, mdwn, mdx, mkd, mkdn, mkdown, ronn, workbook)
Mathematica                (cdf, ma, mathematica, mt, nbp, wl, wlt, m)
MATLAB                     (m)
Maven                      (pom, pom.xml)
Modula3                    (i3, ig, m3, mg)
MSBuild script             (csproj, vbproj, vcproj, wdproj, wixproj)
MUMPS                      (mps, m)
Mustache                   (mustache)
MXML                       (mxml)
NAnt script                (build)
NASTRAN DMAP               (dmap)
Nemerle                    (n)
Nim                        (nim, nim.cfg, nimble, nimrod, nims)
Nix                        (nix)
Objective C                (m)
Objective C++              (mm)
OCaml                      (eliom, eliomi, ml, ml4, mli, mll, mly)
OpenCL                     (cl)
Oracle Forms               (fmt)
Oracle PL/SQL              (bod, fnc, prc, spc, trg)
Oracle Reports             (rex)
Pascal                     (dfm, dpr, lpr, p, pas, pascal)
Pascal/Puppet              (pp)
Patran Command Language    (pcl, ses)
Perl                       (ack, al, cpanfile, makefile.pl, perl, ph, plh, plx, pm, pm6, psgi, rexfile, pl)
PHP                        (aw, ctp, phakefile, php, php3, php4, php5, php_cs, php_cs.dist, phps, phpt, phtml)
PHP/Pascal                 (inc)
Pig Latin                  (pig)
PL/I                       (pl1)
PL/M                       (lit, plm)
PO File                    (po)
PowerBuilder               (pbt, sra, srf, srm, srs, sru, srw)
PowerShell                 (ps1, psd1, psm1)
ProGuard                   (pro)
Prolog                     (P, prolog, yap, pl, pro)
Protocol Buffers           (proto)
Pug                        (jade, pug)
PureScript                 (purs)
Python                     (buck, build.bazel, gclient, gyp, gypi, lmi, py, py3, pyde, pyi, pyp, pyt, pyw, sconscript, sconstruct, snakefile, tac, workspace, wscript, wsgi, xpy)
QML                        (qbs, qml)
Qt                         (ui)
Qt Linguist                (ts)
Qt Project                 (pro)
R                          (expr-dist, r, R, rd, rprofile, rsx)
Racket                     (rkt, rktd, rktl, scrbl)
RAML                       (raml)
RapydScript                (pyj)
Razor                      (cshtml)
ReasonML                   (re, rei)
reStructuredText           (rest, rest.txt, rst, rst.txt)
Rexx                       (pprx, rexx)
Rmd                        (Rmd)
RobotFramework             (robot, tsv)
Ruby                       (appraisals, berksfile, brewfile, builder, buildfile, capfile, dangerfile, deliverfile, eye, fastfile, gemfile, gemfile.lock, gemspec, god, guardfile, irbrc, jarfile, jbuilder, mavenfile, mspec, podfile, podspec, pryrc, puppetfile, rabl, rake, rb, rbuild, rbw, rbx, ru, snapfile, thor, thorfile, vagrantfile, watchr)
Ruby HTML                  (rhtml)
Rust                       (rs, rs.in)
SaltStack                  (sls)
SAS                        (sas)
Sass                       (sass, scss)
Scala                      (kojo, sbt, scala)
Scheme                     (sc, sch, scm, sld, sps, ss, sls)
sed                        (sed)
SKILL                      (il)
SKILL++                    (ils)
Slice                      (ice)
Slim                       (slim)
Smalltalk                  (st, cs)
Smarty                     (smarty, tpl)
Softbridge Basic           (sbl, SBL)
Solidity                   (sol)
SparForte                  (sp)
Specman e                  (e)
SQL                        (cql, mysql, psql, sql, SQL, tab, udf, viw)
SQL Data                   (data.sql)
SQL Stored Procedure       (spc.sql, spoc.sql, sproc.sql, udf.sql)
Standard ML                (fun, sig, sml)
Starlark                   (bzl)
Stata                      (ado, do, DO, doh, ihlp, mata, matah, sthlp)
Stylus                     (styl)
SVG                        (svg, SVG)
Swift                      (swift)
SWIG                       (i)
Tcl/Tk                     (itk, tcl, tk)
Teamcenter met             (met)
Teamcenter mth             (mth)
TeX                        (aux, bbx, bib, bst, cbx, dtx, ins, lbx, ltx, mkii, mkiv, mkvi, sty, tex, cls)
Thrift                     (thrift)
TITAN Project File Information (tpd)
Titanium Style Sheet       (tss)
TOML                       (toml)
TTCN                       (ttcn, ttcn2, ttcn3, ttcnpp)
Twig                       (twig)
TypeScript                 (tsx, ts)
Unity-Prefab               (mat, prefab)
Vala                       (vala)
Vala Header                (vapi)
Velocity Template Language (vm)
Verilog-SystemVerilog      (sv, svh, v)
VHDL                       (VHD, vhd, vhdl, VHDL, vhf, vhi, vho, vhs, vht, vhw)
vim script                 (vim)
Visual Basic               (bas, ctl, dsr, frm, frx, vb, VB, VBA, vba, vbhtml, vbs, VBS, cls)
Visual Fox Pro             (SCA, sca)
Visualforce Component      (component)
Visualforce Page           (page)
Vuejs Component            (vue)
WebAssembly                (wast, wat)
Windows Message File       (mc)
Windows Module Definition  (def)
Windows Resource File      (rc, rc2)
WiX include                (wxi)
WiX source                 (wxs)
WiX string localization    (wxl)
XAML                       (xaml)
xBase                      (prg, prw)
xBase Header               (ch)
XHTML                      (xhtml)
XMI                        (xmi, XMI)
XML                        (adml, admx, ant, app.config, axml, builds, ccproj, ccxml, classpath, clixml, cproject, cscfg, csdef, csl, ct, depproj, ditamap, ditaval, dll.config, dotsettings, filters, fsproj, gmx, grxml, iml, ivy, jelly, jsproj, kml, launch, mdpolicy, mjml, natvis, ndproj, nproj, nuget.config, nuspec, odd, osm, packages.config, pkgproj, plist, proj, project, props, ps1xml, psc1, pt, rdf, resx, rss, scxml, settings.stylecop, sfproj, shproj, srdf, storyboard, sttheme, sublime-snippet, targets, tmcommand, tml, tmlanguage, tmpreferences, tmsnippet, tmtheme, urdf, ux, vcxproj, vsixmanifest, vssettings, vstemplate, vxml, web.config, web.debug.config, web.release.config, wsf, x3d, xacro, xib, xlf, xliff, XML, xml, xml.dist, xproj, xspec, xul, zcml)
XQuery                     (xq, xql, xqm, xquery, xqy)
XSD                        (xsd, XSD)
XSLT                       (XSL, xsl, xslt, XSLT)
Xtend                      (xtend)
yacc                       (y, yacc)
YAML                       (clang-format, clang-tidy, gemrc, glide.lock, mir, reek, rviz, sublime-syntax, syntax, yaml, yaml-tmlanguage, yml, yml.mysql)
zsh                        (zsh)
</pre>

上面的列表可以通过使用`--read-lang-def`或`--force-lang-def`选项从一个文件中读取语言定义来定制。

These file extensions map to multiple languages:

*   `cl`  files could be Lisp or OpenCL
*   `cls` files could be Visual Basic, TeX or Apex Class
*   `cs`  files could be C# or Smalltalk
*   `d`   files could be D or dtrace
*   `f`   files could be Fortran 77 or Forth
*   `fnc` files could be Oracle PL or SQL
*   `for` files could be Fortran 77 or Forth
*   `fs`  files could be F# or Forth
*   `inc` files could be PHP or Pascal
*   `itk` files could be Tcl or Tk
*   `jl`  files could be Lisp or Julia
*   `lit` files could be PL or M
*   `m`   files could be MATLAB, Mathematica, Objective C, MUMPS or Mercury
*   `p6`  files could be Perl or Prolog
*   `pl`  files could be Perl or Prolog
*   `PL`  files could be Perl or Prolog
*   `pp`  files could be Pascal or Puppet
*   `pro` files could be IDL, Qt Project, Prolog or ProGuard
*   `ts`  files could be TypeScript or Qt Linguist
*   `ui`  files could be Qt or Glade
*   `v`   files could be Verilog-SystemVerilog or Coq

cloc有一些子程序，试图根据文件的内容来识别这些特殊情况下的正确语言
Language identification accuracy is a function of how much code the file contains; .m files with
just one or two lines for example, seldom have enough information to
correctly distinguish between MATLAB, Mercury, MUMPS, or Objective C.

有文件扩展名碰撞的语言很难用 `--read-lang-def` 或 `--force-lang-def` 来定制，因为它们没有机制来识别具有共同扩展名的语言。在这种情况下，我们必须修改 cloc 源代码。
[](1}}})
<a name="How_it_works"></a> []({{{1)
# [它是如何工作的 &#9650;](#___top "click to go to top of document")

cloc的操作方法类似于SLOCCount的操作方法。<br>
首先，创建一个要考虑的文件列表。<br>
接下来，尝试确定所找到的文件是否包含识别的计算机语言源码。<br>
最后，对于被识别为源文件的文件，调用特定语言的例程来计算源码行数。

更详细的说明:

1.  If the input file is an archive (such as a .tar.gz or .zip file),
    create a temporary directory and expand the archive there using a
    system call to an appropriate underlying utility (tar, bzip2, unzip,
    etc) then add this temporary directory as one of the inputs. (This
    works more reliably on Unix than on Windows.)
2.  Use File::Find to recursively descend the input directories and make
    a list of candidate file names. Ignore binary and zero-sized files.
3.  Make sure the files in the candidate list have unique contents
    (first by comparing file sizes, then, for similarly sized files,
    compare MD5 hashes of the file contents with Digest::MD5). For each
    set of identical files, remove all but the first copy, as determined
    by a lexical sort, of identical files from the set. The removed
    files are not included in the report. (The `--skip-uniqueness` switch
    disables the uniqueness tests and forces all copies of files to be
    included in the report.) See also the `--ignored=` switch to see which
    files were ignored and why.
4.  Scan the candidate file list for file extensions which cloc
    associates with programming languages (see the `--show-lang` and
    `--show-ext` options). Files which match are classified as
    containing source
    code for that language. Each file without an extensions is opened
    and its first line read to see if it is a Unix shell script
    (anything that begins with #!). If it is shell script, the file is
    classified by that scripting language (if the language is
    recognized). If the file does not have a recognized extension or is
    not a recognzied scripting language, the file is ignored.
5.  All remaining files in the candidate list should now be source files
    for known programming languages. For each of these files:

    1.  Read the entire file into memory.
    2.  Count the number of lines (= L<sub>original</sub>).
    3.  Remove blank lines, then count again (= L<sub>non_blank</sub>).
    4.  Loop over the comment filters defined for this language. (For
        example, C++ has two filters: (1) remove lines that start with
        optional whitespace followed by // and (2) remove text between
        /* and */) Apply each filter to the code to remove comments.
        Count the left over lines (= L<sub>code</sub>).
    5.  Save the counts for this language:
        * blank lines = L<sub>original</sub> - L<sub>non_blank</sub>
        * comment lines = L<sub>non_blank</sub> - L<sub>code</sub>
        * code lines = L<sub>code</sub>

这些选项稍微修改了算法。<br>
例如`--read-lang-def`选项允许用户从文件中读取注释过滤器的定义、已知的文件扩展名和已知的脚本语言。这个选项的代码在处理步骤2和3之间。
[](1}}})
<a name="Advanced_Use"></a> []({{{1)
# [高级用法 &#9650;](#___top "click to go to top of document")
[](1}}})
<a name="strip_comments"></a> []({{{1)
##  [从源码中删除注释 &#9650;](#___top "click to go to top of document")

如何判断cloc是否正确识别注释？一个让自己相信cloc做得对的方法是使用它的`--strip-comments`选项来删除文件中的注释和空行，然后将剥离后的文件与原始文件进行比较。

让我们用SQLite amalgamation来试试，这个C文件包含了构建SQLite库所需的所有代码和头文件.

<pre>
prompt> tar zxf sqlite-amalgamation-3.5.6.tar.gz
prompt> cd sqlite-3.5.6/
prompt> cloc --strip-comments=nc sqlite.c
       1 text file.
       1 unique file.
Wrote sqlite3.c.nc
       0 files ignored.

http://cloc.sourceforge.net v 1.03  T=1.0 s (1.0 files/s, 82895.0 lines/s)
-------------------------------------------------------------------------------
Language          files     blank   comment      code    scale   3rd gen. equiv
-------------------------------------------------------------------------------
C                     1      5167     26827     50901 x   0.77 =       39193.77
-------------------------------------------------------------------------------
</pre>

给予 --strip-comments 的扩展参数是任意的；这里 nc 被用作 "无注释"的缩写 .

cloc从文件中删除了31 000多行:

<pre>
prompt> wc -l sqlite3.c sqlite3.c.nc
  82895 sqlite3.c
  50901 sqlite3.c.nc
 133796 total
prompt> echo "82895 - 50901" | bc
31994
</pre>

现在我们可以用diff或vimdiff等工具来比较原始文件sqlite3.c和被剥离了注释的文件sqlite3.c.nc，看看cloc到底认为注释和空行是什么。一个严格的证明被剥离的文件包含与原文件相同的C语言代码的方法是编译这些文件，并比较所产生的对象文件的校验和.

首先，原始源文件:

<pre>
prompt> gcc -c sqlite3.c
prompt> md5sum sqlite3.o
cce5f1a2ea27c7e44b2e1047e2588b49  sqlite3.o
</pre>

接下来是没有注解的版本:

<pre>
prompt> mv sqlite3.c.nc sqlite3.c
prompt> gcc -c sqlite3.c
prompt> md5sum sqlite3.o
cce5f1a2ea27c7e44b2e1047e2588b49  sqlite3.o
</pre>

cloc删除了31,000多行注释和空白，但并没有对源代码进行任何重大修改，因为生成的对象文件与原始的.
[](1}}})
<a name="compressed_arch"></a> []({{{1)
##  [使用压缩档案 &#9650;](#___top "click to go to top of document")
在v1.07之前的cloc版本需要使用`--extract-with=CMD`选项，告诉cloc如何使用来扩展一个存档文件。 
从v1.07版本开始，这种提取方法会自动进行。 
目前，自动提取方法在Unix类型的操作系统上运行良好，适用于以下文件类型:
`.tar.gz`,
`.tar.bz2`,
`.tar.xz`,
`.tgz`,
`.zip`,
`.ear`,
`.deb`.
如果你在默认位置安装了WinZip，其中一些扩展程序可以在Windows上工作 (`C:\Program Files\WinZip\WinZip32.exe`).
此外，对于较新版本的WinZip，[http://www.winzip.com/downcl.htm](命令行插件)
需要正确的操作;<br>
在这个例子里面，cloc的调用如下 <br>
<pre>
 --extract-with="\"c:\Program Files\WinZip\wzunzip\" -e -o &gt;FILE&lt; ."
 </code>
</pre>
Ref. http://sourceforge.net/projects/cloc/forums/forum/600963/topic/4021070?message=8938196

在自动提取失败的情况下，可以尝试使用 `--extract-with=CMD` 选项来计算 tar 文件、Zip 文件或 其他有提取工具的压缩档案。

cloc 读取用户提供的提取命令，并扩展存档。到一个临时目录（created with File::Temp）。计算临时目录中的代码行数。然后删除该目录。 

虽然在处理 与单一的压缩存档（毕竟，如果你要输入 拔出命令，为什么不直接手动扩展存档？) 这个选项对于同时处理多个存档是很方便的。

例如，假设你在一台Unix机器上有以下的源码包<br>

    perl-5.8.5.tar.gz
    Python-2.4.2.tar.gz

而你想计算其中的所有代码。 该命令将是
<pre>
cloc --extract-with='gzip -dc &gt;FILE&lt; | tar xf -' perl-5.8.5.tar.gz Python-2.4.2.tar.gz
</pre>
如果Unix机器有GNU tar (可以一步到位地解压和释放) 该命令简称为
<pre>
cloc --extract-with='tar zxf &gt;FILE&lt;' perl-5.8.5.tar.gz Python-2.4.2.tar.gz
</pre>
在安装了WinZip的Windows电脑上，在`c:\Program Files\WinZip`中安装了WinZip命令，该命令看起来像这样
<pre>
cloc.exe --extract-with="\"c:\Program Files\WinZip\WinZip32.exe\" -e -o &gt;FILE&lt; ." perl-5.8.5.tar.gz Python-2.4.2.tar.gz
</pre>
Java `.ear` files are Zip files that contain additional Zip
files.  cloc can handle nested compressed archives without
difficulty--provided all such files are compressed and archived in the
same way.  
Examples of counting a Java `.ear` file in Unix and Windows:
<pre>
<i>Unix&gt;</i> cloc --extract-with="unzip -d . &gt;FILE&lt; " Project.ear
<i>DOS&gt;</i> cloc.exe --extract-with="\"c:\Program Files\WinZip\WinZip32.exe\" -e -o &gt;FILE&lt; ." Project.ear
</pre>

[](1}}})
<a name="diff"></a> []({{{1)
##  [差异性 &#9650;](#___top "click to go to top of document")
The `--diff` switch allows one to measure the relative change in
source code and comments between two versions of a file, directory,
or archive.  Differences reveal much more than absolute code
counts of two file versions.  For example, say a source file
has 100 lines and its developer delivers a newer version with
102 lines.  Did the developer add two comment lines,
or delete seventeen source
lines and add fourteen source lines and five comment lines, or did
the developer
do a complete rewrite, discarding all 100 original lines and
adding 102 lines of all new source?  The diff option tells how
many lines of source were added, removed, modified or stayed
the same, and how many lines of comments were added, removed,
modified or stayed the same.

空白行的差异会被更粗略地处理，因为cloc会在早期剥离这些差异。 除非一个文件对是相同的，否则cloc只会报告空行的绝对数的差异。 换句话说，如果第二个文件的空白行数比第一个文件多，我们可以期望只看到 "添加 "的条目，如果情况相反，则会看到 "删除 "的条目。 只有当两个文件完全相同时，"相同 "的条目才会是非零。

In addition to file pairs, one can give cloc pairs of
directories, or pairs of file archives, or a file archive
and a directory.  cloc will try to align
file pairs within the directories or archives and compare diffs
for each pair.  For example, to see what changed between
GCC 4.4.0 and 4.5.0 one could do
<pre>
cloc --diff gcc-4.4.0.tar.bz2  gcc-4.5.0.tar.bz2
</pre>

Be prepared to wait a while for the results though; the `--diff`
option runs much more slowly than an absolute code count.

To see how cloc aligns files between the two archives, use the
`--diff-alignment` option
<pre>
cloc --diff-aligment=align.txt gcc-4.4.0.tar.bz2  gcc-4.5.0.tar.bz2
</pre>
to produce the file `align.txt` which shows the file pairs as well
as files added and deleted.  The symbols `==` and `!=` before each
file pair indicate if the files are identical (`==`)
or if they have different content (`!=`).

以下是显示Python 2.6.6 和2.7版本之间差异的输出示例:
<pre><i>prompt&gt;</i> cloc --diff Python-2.7.9.tgz Python-2.7.10.tar.xz
    4315 text files.
    4313 text files.s
    2173 files ignored.

4 errors:
Diff error, exceeded timeout:  /tmp/8ToGAnB9Y1/Python-2.7.9/Mac/Modules/qt/_Qtmodule.c
Diff error, exceeded timeout:  /tmp/M6ldvsGaoq/Python-2.7.10/Mac/Modules/qt/_Qtmodule.c
Diff error (quoted comments?):  /tmp/8ToGAnB9Y1/Python-2.7.9/Mac/Modules/qd/qdsupport.py
Diff error (quoted comments?):  /tmp/M6ldvsGaoq/Python-2.7.10/Mac/Modules/qd/qdsupport.py

https://github.com/AlDanial/cloc v 1.65  T=298.59 s (0.0 files/s, 0.0 lines/s)
-----------------------------------------------------------------------------
Language                   files          blank        comment           code
-----------------------------------------------------------------------------
Visual Basic
 same                          2              0              1             12
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
make
 same                         11              0            340           2952
 modified                      1              0              0              1
 added                         0              0              0              0
 removed                       0              0              0              0
diff
 same                          1              0             87            105
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
CSS
 same                          0              0             19            327
 modified                      1              0              0              1
 added                         0              0              0              0
 removed                       0              0              0              0
Objective C
 same                          7              0             61            635
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
NAnt script
 same                          2              0              0             30
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
XML
 same                          3              0              2             72
 modified                      1              0              0              1
 added                         0              0              0              1
 removed                       0              1              0              0
Windows Resource File
 same                          3              0             56            206
 modified                      1              0              0              1
 added                         0              0              0              0
 removed                       0              0              0              0
Expect
 same                          6              0            161            565
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
HTML
 same                         14              0             11           2344
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
vim script
 same                          1              0              7            106
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
C++
 same                          2              0             18            128
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
Windows Module Definition
 same                          7              0            187           2080
 modified                      2              0              0              0
 added                         0              0              0              1
 removed                       0              1              0              2
Prolog
 same                          1              0              0             24
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
Javascript
 same                          3              0             49            229
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
Assembly
 same                         51              0           6794          12298
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
Bourne Shell
 same                         41              0           7698          45024
 modified                      1              0              0              3
 added                         0             13              2             64
 removed                       0              0              0              0
DOS Batch
 same                         29              0            107            494
 modified                      1              0              0              9
 added                         0              1              0              3
 removed                       0              0              0              0
MSBuild script
 same                         77              0              3          38910
 modified                      0              0              0              0
 added                         0              0              0              0
 removed                       0              0              0              0
Python
 same                       1947              0         109012         430335
 modified                    192              0             94            950
 added                         2            323            283           2532
 removed                       2             55             58            646
m4
 same                         18              0            191          15352
 modified                      1              0              0              2
 added                         1             31              0            205
 removed                       0              0              0              0
C
 same                        505              0          37439         347837
 modified                     45              0             13            218
 added                         0             90             33            795
 removed                       0              9              2            148
C/C++ Header
 same                        255              0          10361          66635
 modified                      5              0              5              7
 added                         0              1              3            300
 removed                       0              0              0              0
---------------------------------------------------------------------
SUM:
 same                       2986              0         172604         966700
 modified                    251              0            112           1193
 added                         3            459            321           3901
 removed                       2             66             60            796
---------------------------------------------------------------------
</pre>
A pair of errors occurred.
The first pair was caused by timing out when computing diffs of the file
`Python-X/Mac/Modules/qt/_Qtmodule.c` in each Python version.
This file has > 26,000 lines of C code and takes more than
10 seconds--the default maximum duration for diff'ing a
single file--on my slow computer.  (Note:  this refers to
performing differences with
the `sdiff()` function in the Perl `Algorithm::Diff` module,
not the command line `diff` utility.)  This error can be
overcome by raising the time to, say, 20 seconds
with `--diff-timeout 20`.

The second error is more problematic.  The files
`Python-X/Mac/Modules/qd/qdsupport.py`
include Python docstring (text between pairs of triple quotes)
containing C comments.  cloc treats docstrings as comments and handles them
by first converting them to C comments, then using the C comment removing
regular expression.  Nested C comments yield erroneous results however.

[](1}}})
<a name="custom_lang"></a> []({{{1)
##  [创建自定义语言的定义  &#9650;](#___top "click to go to top of document")
cloc可以将语言注释定义写入文件，或者从文件中读取注释定义，覆盖内置定义。
当你想用cloc来计算还没有包含的语言的行数，改变文件扩展名与语言的关联，或者修改现有语言的计算方式时，这可能很有用。

创建自定义语言定义文件的最简单方法是让cloc将其定义写到一个文件中，然后修改该文件:
<pre><i>Unix&gt;</i> cloc --write-lang-def=my_definitions.txt
</pre>
creates the file `my_definitions.txt` which can be modified
then read back in with either the `--read-lang-def` or
`--force-lang-def` option.  The difference between the options is
former merges language definitions from the given file in with
cloc's internal definitions with cloc's taking precedence
if there are overlaps.  The `--force-lang-def` option, on the
other hand, replaces cloc's definitions completely.
This option has a disadvantage in preventing cloc from counting
<a class="u" href="#extcollision" name="extcollision">
languages whose extensions map to multiple languages
</a> as these languages require additional logic that is not easily
expressed in a definitions file.
<pre><i>Unix&gt;</i> cloc --read-lang-def=my_definitions.txt  <i>file1 file2 dir1 ...</i>
</pre>

Each language entry has four parts:
* The language name starting in column 1.
* One or more comment *filters* starting in column 5.
* One or more filename extensions starting in column 5.
* A 3rd generation scale factor starting in column 5.
  This entry must be provided
  but its value is not important
  unless you want to compare your language to a hypothetical
  third generation programming language.

过滤器定义了一种方法来删除源文件中的注释文本。
例如，C++的条目是这样的
<pre>C++
    filter call_regexp_common C++
    filter remove_inline //.*$
    extension C
    extension c++
    extension cc
    extension cpp
    extension cxx
    extension pcc
    3rd_gen_scale 1.51
    end_of_line_continuation \\$
</pre>
C++ has two filters:  first, remove lines matching
Regexp::Common's C++ comment regex.
The second filter using remove_inline is currently
unused.  Its intent is to identify lines with both
code and comments and it may be implemented in the future.

A more complete discussion of the different filter options may appear
here in the future.  The output of cloc's
`--write-lang-def` option should provide enough examples
for motivated individuals to modify or extend cloc's language definitions.

[](1}}})
<a name="combine_reports"></a> []({{{1)
##  [合并报告 &#9650;](#___top "click to go to top of document")

如果你管理多个软件项目，你可能会有兴趣看到按项目，而不仅仅是按语言分类的行数。.
假设你管理三个软件项目，分别是MariaDB、PostgreSQL和SQLite.
负责这些项目的团队会在他们的源代码上运行 cloc，并为您提供输出.
For example MariaDB team does

<pre>cloc --out mariadb-10.1.txt mariadb-server-10.1.zip</pre>

and provides you with the file `mariadb-10.1.txt`.
你得到的三个文件的内容是

<pre>
<i>Unix&gt;</i> cat mariadb-10.1.txt
https://github.com/AlDanial/cloc v 1.65  T=45.36 s (110.5 files/s, 66411.4 lines/s)
-----------------------------------------------------------------------------------
Language                         files          blank        comment           code
-----------------------------------------------------------------------------------
C++                               1613         225338         290077         983026
C                                  853          62442          73017         715018
C/C++ Header                      1327          48300         114577         209394
Bourne Shell                       256          10224          10810          61943
Perl                               147          10342           8305          35562
Pascal                             107           4907           5237          32541
HTML                                56            195              6          16489
Javascript                           5           3309           3019          15540
m4                                  30           1599            359          14215
CMake                              190           1919           4097          12206
XML                                 35            648             56           5210
Ruby                                59            619            184           4998
Puppet                              10              0              1           3848
make                               134            724            360           3631
SQL                                 23            306            377           3405
Python                              34            371            122           2545
Bourne Again Shell                  27            299            380           1604
Windows Module Definition           37             27             13           1211
lex                                  4            394            166            991
yacc                                 2            152             64            810
DOS Batch                           19             89             82            700
Prolog                               1              9             40            448
RobotFramework                       1              0              0            441
CSS                                  2             33            155            393
JSON                                 5              0              0            359
dtrace                               9             59            179            306
Windows Resource File               10             61             89            250
Assembly                             2             70            284            237
WiX source                           1             18             10            155
Visual Basic                         6              0              0             88
YAML                                 2              4              4             65
PHP                                  1             11              2             24
SKILL                                1              8             15             16
sed                                  2              0              0             16
Windows Message File                 1              2              8              6
diff                                 1              1              4              4
D                                    1              4             11              4
-----------------------------------------------------------------------------------
SUM:                              5014         372484         512110        2127699
-----------------------------------------------------------------------------------

<i>Unix&gt;</i> cat sqlite-3081101.txt
https://github.com/AlDanial/cloc v 1.65  T=1.22 s (3.3 files/s, 143783.6 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
C                                2          11059          53924         101454
C/C++ Header                     2            211           6630           1546
-------------------------------------------------------------------------------
SUM:                             4          11270          60554         103000
-------------------------------------------------------------------------------

<i>Unix&gt;</i> cat postgresql-9.4.4.txt
https://github.com/AlDanial/cloc v 1.65  T=22.46 s (172.0 files/s, 96721.6 lines/s)
-----------------------------------------------------------------------------------
Language                         files          blank        comment           code
-----------------------------------------------------------------------------------
HTML                              1254           3725              0         785991
C                                 1139         139289         244045         736519
C/C++ Header                       667          12277          32488          57014
SQL                                410          13400           8745          51926
yacc                                 8           3163           2669          28491
Bourne Shell                        41           2647           2440          17170
Perl                                81           1702           1308           9456
lex                                  9            792           1631           4285
make                               205           1525           1554           4114
m4                                  12            218             25           1642
Windows Module Definition           13              4             17           1152
XSLT                                 5             76             55            294
DOS Batch                            7             29             30             92
CSS                                  1             20              7             69
Assembly                             3             17             38             69
D                                    1             14             14             66
Windows Resource File                3              4              0             62
Lisp                                 1              1              1             16
sed                                  1              1              7             15
Python                               1              5              0             13
Bourne Again Shell                   1              8              6             10
Windows Message File                 1              0              0              5
-----------------------------------------------------------------------------------
SUM:                              3864         178917         295080        1698471
-----------------------------------------------------------------------------------
</pre>

虽然这三个文件很有意思，但你也想看看所有项目的综合计数。
这可以用cloc的`--sum_reports`选项来完成:

<pre>
<i>Unix&gt;</i> cloc --sum-reports --out=databases mariadb-10.1.txt  sqlite-3081101.txt  postgresql-9.4.4.txt
Wrote databases.lang
Wrote databases.file
</pre>

报告组合产生两个输出文件,一个是按编程语言 (`databases.lang`)和按项目(`databases.file`)的总和。
<pre><i>Unix&gt;</i> cat databases.lang
https://github.com/AlDanial/cloc v 1.65
--------------------------------------------------------------------------------
Language                      files          blank        comment           code
--------------------------------------------------------------------------------
C                              1994         212790         370986        1552991
C++                            1613         225338         290077         983026
HTML                           1310           3920              6         802480
C/C++ Header                   1996          60788         153695         267954
Bourne Shell                    297          12871          13250          79113
SQL                             433          13706           9122          55331
Perl                            228          12044           9613          45018
Pascal                          107           4907           5237          32541
yacc                             10           3315           2733          29301
m4                               42           1817            384          15857
Javascript                        5           3309           3019          15540
CMake                           190           1919           4097          12206
make                            339           2249           1914           7745
lex                              13           1186           1797           5276
XML                              35            648             56           5210
Ruby                             59            619            184           4998
Puppet                           10              0              1           3848
Python                           35            376            122           2558
Windows Module Definition        50             31             30           2363
Bourne Again Shell               28            307            386           1614
DOS Batch                        26            118            112            792
CSS                               3             53            162            462
Prolog                            1              9             40            448
RobotFramework                    1              0              0            441
JSON                              5              0              0            359
Windows Resource File            13             65             89            312
Assembly                          5             87            322            306
dtrace                            9             59            179            306
XSLT                              5             76             55            294
WiX source                        1             18             10            155
Visual Basic                      6              0              0             88
D                                 2             18             25             70
YAML                              2              4              4             65
sed                               3              1              7             31
PHP                               1             11              2             24
SKILL                             1              8             15             16
Lisp                              1              1              1             16
Windows Message File              2              2              8             11
diff                              1              1              4              4
--------------------------------------------------------------------------------
SUM:                           8882         562671         867744        3929170
--------------------------------------------------------------------------------

<i>Unix&gt;</i> cat databases.file
----------------------------------------------------------------------------------
File                            files          blank        comment           code
----------------------------------------------------------------------------------
mariadb-10.1.txt                 5014         372484         512110        2127699
postgresql-9.4.4.txt             3864         178917         295080        1698471
sqlite-3081101.txt                  4          11270          60554         103000
----------------------------------------------------------------------------------
SUM:                             8882         562671         867744        3929170
----------------------------------------------------------------------------------
</pre>

报告文件本身可以归纳起来。 假设你也管理Perl和Python的开发，你想把这些行数与数据库项目分开来跟踪。 

首先为Perl和Python分别创建报表:

<pre>
cloc --out perl-5.22.0.txt   perl-5.22.0.tar.gz
cloc --out python-2.7.10.txt Python-2.7.10.tar.xz
</pre>

然后加起来

<pre>
<i>Unix&gt;</i> cloc --sum-reports --out script_lang perl-5.22.0.txt python-2.7.10.txt
Wrote script_lang.lang
Wrote script_lang.file

<i>Unix&gt;</i> cat script_lang.lang
https://github.com/AlDanial/cloc v 1.65
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Perl                          2892         136396         184362         536445
C                              680          75566          71211         531203
Python                        2141          89642         109524         434015
C/C++ Header                   408          16433          26938         214800
Bourne Shell                   154          11088          14496          87759
MSBuild script                  77              0              3          38910
m4                              20           1604            191          15559
Assembly                        51           3775           6794          12298
Pascal                           8            458           1603           8592
make                            16            897            828           4939
XML                             37            198              2           2484
HTML                            14            393             11           2344
C++                             12            338            295           2161
Windows Module Definition        9            171            187           2081
YAML                            49             20             15           2078
Prolog                          12            438              2           1146
JSON                            14              1              0           1037
yacc                             1             85             76            998
DOS Batch                       44            199            148            895
Objective C                      7             98             61            635
Expect                           6            104            161            565
Windows Message File             1            102             11            489
CSS                              1             98             19            328
Windows Resource File            7             55             56            292
Javascript                       3             31             49            229
vim script                       1             36              7            106
diff                             1             17             87            105
NAnt script                      2              1              0             30
IDL                              1              0              0             24
Visual Basic                     2              1              1             12
D                                1              5              7              8
Lisp                             2              0              3              4
-------------------------------------------------------------------------------
SUM:                          6674         338250         417148        1902571
-------------------------------------------------------------------------------

<i>Unix&gt;</i> cat script_lang.file
-------------------------------------------------------------------------------
File                         files          blank        comment           code
-------------------------------------------------------------------------------
python-2.7.10.txt             3240         161276         173214         998697
perl-5.22.0.txt               3434         176974         243934         903874
-------------------------------------------------------------------------------
SUM:                          6674         338250         417148        1902571
-------------------------------------------------------------------------------
</pre>

最后，结合组合文件:

<pre>
<i>Unix&gt;</i> cloc --sum-reports --report_file=everything databases.lang script_lang.lang
Wrote everything.lang
Wrote everything.file

<i>Unix&gt;</i> cat everything.lang
https://github.com/AlDanial/cloc v 1.65
---------------------------------------------------------------------------------
Language                       files          blank        comment           code
---------------------------------------------------------------------------------
C                               2674         288356         442197        2084194
C++                             1625         225676         290372         985187
HTML                            1324           4313             17         804824
Perl                            3120         148440         193975         581463
C/C++ Header                    2404          77221         180633         482754
Python                          2176          90018         109646         436573
Bourne Shell                     451          23959          27746         166872
SQL                              433          13706           9122          55331
Pascal                           115           5365           6840          41133
MSBuild script                    77              0              3          38910
m4                                62           3421            575          31416
yacc                              11           3400           2809          30299
Javascript                         8           3340           3068          15769
make                             355           3146           2742          12684
Assembly                          56           3862           7116          12604
CMake                            190           1919           4097          12206
XML                               72            846             58           7694
lex                               13           1186           1797           5276
Ruby                              59            619            184           4998
Windows Module Definition         59            202            217           4444
Puppet                            10              0              1           3848
YAML                              51             24             19           2143
DOS Batch                         70            317            260           1687
Bourne Again Shell                28            307            386           1614
Prolog                            13            447             42           1594
JSON                              19              1              0           1396
CSS                                4            151            181            790
Objective C                        7             98             61            635
Windows Resource File             20            120            145            604
Expect                             6            104            161            565
Windows Message File               3            104             19            500
RobotFramework                     1              0              0            441
dtrace                             9             59            179            306
XSLT                               5             76             55            294
WiX source                         1             18             10            155
diff                               2             18             91            109
vim script                         1             36              7            106
Visual Basic                       8              1              1            100
D                                  3             23             32             78
sed                                3              1              7             31
NAnt script                        2              1              0             30
IDL                                1              0              0             24
PHP                                1             11              2             24
Lisp                               3              1              4             20
SKILL                              1              8             15             16
---------------------------------------------------------------------------------
SUM:                           15556         900921        1284892        5831741
---------------------------------------------------------------------------------

<i>Unix&gt;</i> cat everything.file
-------------------------------------------------------------------------------
File                         files          blank        comment           code
-------------------------------------------------------------------------------
databases.lang                8882         562671         867744        3929170
script_lang.lang              6674         338250         417148        1902571
-------------------------------------------------------------------------------
SUM:                         15556         900921        1284892        5831741
-------------------------------------------------------------------------------
</pre>

`--sum-reports`功能的一个限制是，必须以纯文本格式保存单个计数。
保存为XML、JSON、JSON、YAML或SQL格式的计数，如果在汇总中使用，会产生错误.

[](1}}})
<a name="sql"></a> []({{{1)
##  [SQL &#9650;](#___top "click to go to top of document")
Cloc可以以SQL表创建和插入语句的形式编写结果，用于SQLite、MySQL、PostgreSQL、Oracle或Microsoft SQL等关系型数据库程序。
一旦代码计数信息进入数据库，就可以通过有趣的方式查询和显示这些信息。

一个由 cloc SQL 输出创建的数据库有两个表,
**metadata** and **t**:

Table **metadata**:

|Field     | Type |
|----------|------|
|timestamp | text |
|project   | text |
|elapsed_s | text |

Table **t**:

|Field       | Type   |
|------------|--------|
| project    |text    |
| language   |text    |
| file       |text    |
| nBlank     |integer |
| nComment   |integer |
| nCode      |integer |
| nScaled    |real    |

**metadata**表包含了关于cloc运行时间的信息。 
这`--sql-append`开关允许在一个数据库中合并许多运行，每一次运行都会在元数据表中增加一个row。
代码计数信息驻留在表**t**中

让我们重复一下Perl、Python、SQLite、MySQL和PostgreSQL tarballs的代码计数示例，如所示。
[Combine Reports](#combine_reports)
example above, this time
using the SQL output options and the
[SQLite](http://www.sqlite.org/)
database engine.

The `--sql` switch tells cloc to generate output in the form
of SQL table `create` and `insert` commands.  The switch takes
an argument of a file name to write these SQL statements into, or,
if the argument is 1 (numeric one), streams output to STDOUT.
Since the SQLite command line program, `sqlite3`, can read
commands from STDIN, we can dispense with storing SQL statements to
a file and use `--sql 1` to pipe data directly into the
SQLite executable:

<pre>
cloc --sql 1 --sql-project mariadb mariadb-server-10.1.zip | sqlite3 code.db
</pre>

这`--sql-project mariadb`部分是可选的，不需要
当只使用一个代码库时，可以指定一个项目名称。 
但是，由于我们将从其他四个代码库中添加代码计数，所以只有为每一次运行提供一个项目名称，我们才能通过输入源来识别数据。

现在我们有了一个数据库，我们需要通过`--sql-append`开关来告诉cloc不要删除这个数据库，而是增加更多的数据:

<pre>
cloc --sql 1 --sql-project postgresql --sql-append postgresql-9.4.4.tar.bz2        | sqlite3 code.db
cloc --sql 1 --sql-project sqlite     --sql-append sqlite-amalgamation-3081101.zip | sqlite3 code.db
cloc --sql 1 --sql-project python     --sql-append Python-2.7.10.tar.xz            | sqlite3 code.db
cloc --sql 1 --sql-project perl       --sql-append perl-5.22.0.tar.gz              | sqlite3 code.db
</pre>

现在有趣的事情开始了 -- 我们有一个数据库，`code.db`，里面有很多关于这五个项目的信息，可以查询到对于各种有趣的事实.

**在所有的项目中，哪一个是最长的文件？**

<pre>
prompt> sqlite3 code.db 'select project,file,nBlank+nComment+nCode as nL from t
                                 where nL = (select max(nBlank+nComment+nCode) from t)'

sqlite|sqlite-amalgamation-3081101/sqlite3.c|161623
</pre>

`sqlite3`的默认输出格式有一点不尽如人意。
我们可以在程序的rc文件`~/.sqliteerc`中添加一个选项来显示列标题:
<pre>
  .header on
</pre>
人们可能会想把
<pre>
  .mode column
</pre>
在`~/.sqliterc`里面，但当输出有多于一行时，这就会造成问题，因为第一行的条目宽度决定了后面所有行的最大宽度。这通常会导致输出被截断--这并不可取。
一种方法是编写一个自定义的SQLite输出格式化器，比如`sqlite_formatter`，包含在cloc中.

要使用它, 简单地通过 `sqlite3`'s STDOUT into `sqlite_formatter`
via a pipe:

<pre>
prompt> sqlite3 code.db 'select project,file,nBlank+nComment+nCode as nL from t
                         where nL = (select max(nBlank+nComment+nCode) from t)' | ./sqlite_formatter
  <font color="darkgreen">
  -- Loading resources from ~/.sqliterc
  Project File                                  nL
  _______ _____________________________________ ______
  sqlite  sqlite-amalgamation-3081101/sqlite3.c 161623
  </font>
</pre>

If the "Project File" line doesn't appear, add `.header on` to your
`~/.sqliterc` file 如上所述.


**所有项目中最长的文件是什么?**

<pre>
prompt> sqlite3 code.db 'select project,file,nBlank+nComment+nCode as nL from t
                         where nL = (select max(nBlank+nComment+nCode) from t)' | sqlite_formatter

Project File                                  nL
_______ _____________________________________ ______
sqlite  sqlite-amalgamation-3081101/sqlite3.c 161623
</pre>

**每个项目中最长的文件是什么?**

<pre>
prompt> sqlite3 code.db 'select project,file,max(nBlank+nComment+nCode) as nL from t
                          group by project order by nL;' | sqlite_formatter

Project    File                                                             nL
__________ ________________________________________________________________ ______
python     Python-2.7.10/Mac/Modules/qt/_Qtmodule.c                          28091
postgresql postgresql-9.4.4/src/interfaces/ecpg/preproc/preproc.c            54623
mariadb    server-10.1/storage/mroonga/vendor/groonga/lib/nfkc.c             80246
perl       perl-5.22.0/cpan/Locale-Codes/lib/Locale/Codes/Language_Codes.pm 100747
sqlite     sqlite-amalgamation-3081101/sqlite3.c                            161623
</pre>

**每个项目中哪些文件的代码行数最多?**

<pre>
prompt> sqlite3 code.db 'select project,file,max(nCode) as nL from t
                         group by project order by nL desc;' | sqlite_formatter

Project    File                                                             nL
__________ ________________________________________________________________ ______
perl       perl-5.22.0/cpan/Locale-Codes/lib/Locale/Codes/Language_Codes.pm 100735
sqlite     sqlite-amalgamation-3081101/sqlite3.c                             97469
mariadb    server-10.1/storage/mroonga/vendor/groonga/lib/nfkc.c             80221
postgresql postgresql-9.4.4/src/interfaces/ecpg/preproc/preproc.c            45297
python     Python-2.7.10/Mac/Modules/qt/_Qtmodule.c                          26705
</pre>

**哪些300行以上的C源文件的注释率低于1%?**

<pre>
prompt> sqlite3 code.db 'select project, file, nCode, nComment,
                         (100.0*nComment)/(nComment+nCode) as comment_ratio from t
                         where language="C" and nCode > 300 and
                         comment_ratio < 1 order by comment_ratio;' | sqlite_formatter

Project    File                                                                                            nCode nComment comment_ratio
__________ _______________________________________________________________________________________________ _____ ________ __________________
mariadb    server-10.1/storage/mroonga/vendor/groonga/lib/nfkc.c                                           80221       14 0.0174487443135789
python     Python-2.7.10/Python/graminit.c                                                                  2175        1 0.0459558823529412
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_turkish.c                            2095        1 0.0477099236641221
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_french.c                             1211        1 0.0825082508250825
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_french.c                        1201        1 0.0831946755407654
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_hungarian.c                          1182        1 0.084530853761623
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_hungarian.c                     1178        1 0.0848176420695505
mariadb    server-10.1/strings/ctype-eucjpms.c                                                             67466       60 0.0888546633889169
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_english.c                            1072        1 0.0931966449207828
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_english.c                       1064        1 0.0938967136150235
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_spanish.c                            1053        1 0.094876660341556
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_spanish.c                       1049        1 0.0952380952380952
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_italian.c                            1031        1 0.0968992248062016
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_italian.c                       1023        1 0.09765625
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_portuguese.c                          981        1 0.10183299389002
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_portuguese.c                     975        1 0.102459016393443
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_romanian.c                            967        1 0.103305785123967
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_2_romanian.c                       961        1 0.103950103950104
mariadb    server-10.1/strings/ctype-ujis.c                                                                67177       79 0.117461639110265
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_finnish.c                             720        1 0.13869625520111
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_porter.c                              717        1 0.139275766016713
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_finnish.c                        714        1 0.13986013986014
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_porter.c                         711        1 0.140449438202247
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_KOI8_R_russian.c                            660        1 0.151285930408472
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_russian.c                             654        1 0.152671755725191
python     Python-2.7.10/Mac/Modules/qt/_Qtmodule.c                                                        26705       42 0.157026956294164
python     Python-2.7.10/Mac/Modules/icn/_Icnmodule.c                                                       1521        3 0.196850393700787
mariadb    server-10.1/strings/ctype-extra.c                                                                8282       18 0.216867469879518
postgresql postgresql-9.4.4/src/bin/psql/sql_help.c                                                         3576        8 0.223214285714286
mariadb    server-10.1/strings/ctype-sjis.c                                                                34006       86 0.252258594391646
python     Python-2.7.10/Python/Python-ast.c                                                                6554       17 0.258712524729874
mariadb    server-10.1/strings/ctype-cp932.c                                                               34609       92 0.265122042592432
perl       perl-5.22.0/keywords.c                                                                           2815        8 0.283386468296139
python     Python-2.7.10/Mac/Modules/menu/_Menumodule.c                                                     3263       10 0.305530094714329
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_dutch.c                               596        2 0.334448160535117
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_dutch.c                          586        2 0.340136054421769
mariadb    server-10.1/strings/ctype-gbk.c                                                                 10684       38 0.354411490393583
python     Python-2.7.10/Mac/Modules/qd/_Qdmodule.c                                                         6694       24 0.357249181303959
python     Python-2.7.10/Mac/Modules/win/_Winmodule.c                                                       3056       11 0.358656667753505
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_german.c                              476        2 0.418410041841004
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_german.c                         470        2 0.423728813559322
mariadb    server-10.1/strings/ctype-euc_kr.c                                                               9956       44 0.44
postgresql postgresql-9.4.4/src/backend/utils/fmgrtab.c                                                     4815       23 0.475403059115337
python     Python-2.7.10/Mac/Modules/ctl/_Ctlmodule.c                                                       5442       28 0.511882998171846
python     Python-2.7.10/Mac/Modules/ae/_AEmodule.c                                                         1347        7 0.51698670605613
python     Python-2.7.10/Mac/Modules/app/_Appmodule.c                                                       1712        9 0.52295177222545
mariadb    server-10.1/strings/ctype-gb2312.c                                                               6377       35 0.54585152838428
mariadb    server-10.1/storage/tokudb/ft-index/third_party/xz-4.999.9beta/src/liblzma/lzma/fastpos_table.c   516        3 0.578034682080925
python     Python-2.7.10/Mac/Modules/evt/_Evtmodule.c                                                        504        3 0.591715976331361
python     Python-2.7.10/Modules/expat/xmlrole.c                                                            1256        8 0.632911392405063
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_UTF_8_danish.c                              312        2 0.636942675159236
postgresql postgresql-9.4.4/src/backend/snowball/libstemmer/stem_ISO_8859_1_danish.c                         310        2 0.641025641025641
python     Python-2.7.10/Mac/Modules/res/_Resmodule.c                                                       1621       12 0.734843845682792
python     Python-2.7.10/Mac/Modules/drag/_Dragmodule.c                                                     1046        8 0.759013282732448
python     Python-2.7.10/Mac/Modules/list/_Listmodule.c                                                     1021        8 0.777453838678329
python     Python-2.7.10/Mac/Modules/te/_TEmodule.c                                                         1198       10 0.827814569536424
python     Python-2.7.10/Mac/Modules/cg/_CGmodule.c                                                         1190       10 0.833333333333333
python     Python-2.7.10/Modules/clmodule.c                                                                 2379       23 0.957535387177352
python     Python-2.7.10/Mac/Modules/folder/_Foldermodule.c                                                  306        3 0.970873786407767
</pre>

**十个最长的文件（根据代码行数计算）中没有注释的文件有哪些?  排除 header .html 和 YAML文件**

<pre>
prompt> sqlite3 code.db 'select project, file, nCode from t
                         where nComment = 0 and
                         language not in ("C/C++ Header", "YAML", "HTML")
                         order by nCode desc limit 10;' | sqlite_formatter

Project File                                                                 nCode
_______ ____________________________________________________________________ _____
perl    perl-5.22.0/cpan/Unicode-Collate/Collate/Locale/ja.pl                 1938
python  Python-2.7.10/PCbuild/pythoncore.vcproj                               1889
python  Python-2.7.10/PC/VS8.0/pythoncore.vcproj                              1889
mariadb server-10.1/mysql-test/extra/binlog_tests/mysqlbinlog_row_engine.inc  1862
perl    perl-5.22.0/cpan/Unicode-Collate/Collate/Locale/zh_strk.pl            1589
perl    perl-5.22.0/cpan/Unicode-Collate/Collate/Locale/zh_zhu.pl             1563
mariadb server-10.1/storage/mroonga/vendor/groonga/configure.ac               1526
perl    perl-5.22.0/cpan/Unicode-Collate/Collate/Locale/zh_pin.pl             1505
mariadb server-10.1/mysql-test/suite/funcs_1/storedproc/storedproc_02.inc     1465
python  Python-2.7.10/PC/VS8.0/_bsddb.vcproj                                  1463
</pre>

**每个项目中最受欢迎的语言（按代码行数计算）有哪些?**

<pre>
prompt> sqlite3 code.db 'select project, language, sum(nCode) as SumCode from t
                         group by project,language
                         order by project,SumCode desc;' | sqlite_formatter
Project    Language                  SumCode
__________ _________________________ _______
mariadb    C++                        983026
mariadb    C                          715018
mariadb    C/C++ Header               209394
mariadb    Bourne Shell                61943
mariadb    Perl                        35562
mariadb    Pascal                      32541
mariadb    HTML                        16489
mariadb    Javascript                  15540
mariadb    m4                          14215
mariadb    CMake                       12206
mariadb    XML                          5210
mariadb    Ruby                         4998
mariadb    Puppet                       3848
mariadb    make                         3631
mariadb    SQL                          3405
mariadb    Python                       2545
mariadb    Bourne Again Shell           1604
mariadb    Windows Module Definition    1211
mariadb    lex                           991
mariadb    yacc                          810
mariadb    DOS Batch                     700
mariadb    Prolog                        448
mariadb    RobotFramework                441
mariadb    CSS                           393
mariadb    JSON                          359
mariadb    dtrace                        306
mariadb    Windows Resource File         250
mariadb    Assembly                      237
mariadb    WiX source                    155
mariadb    Visual Basic                   88
mariadb    YAML                           65
mariadb    PHP                            24
mariadb    SKILL                          16
mariadb    sed                            16
mariadb    Windows Message File            6
mariadb    D                               4
mariadb    diff                            4
perl       Perl                       536445
perl       C                          155648
perl       C/C++ Header               147858
perl       Bourne Shell                42668
perl       Pascal                       8592
perl       XML                          2410
perl       YAML                         2078
perl       C++                          2033
perl       make                         1986
perl       Prolog                       1146
perl       JSON                         1037
perl       yacc                          998
perl       Windows Message File          489
perl       DOS Batch                     389
perl       Windows Resource File          85
perl       D                               8
perl       Lisp                            4
postgresql HTML                       785991
postgresql C                          736519
postgresql C/C++ Header                57014
postgresql SQL                         51926
postgresql yacc                        28491
postgresql Bourne Shell                17170
postgresql Perl                         9456
postgresql lex                          4285
postgresql make                         4114
postgresql m4                           1642
postgresql Windows Module Definition    1152
postgresql XSLT                          294
postgresql DOS Batch                      92
postgresql Assembly                       69
postgresql CSS                            69
postgresql D                              66
postgresql Windows Resource File          62
postgresql Lisp                           16
postgresql sed                            15
postgresql Python                         13
postgresql Bourne Again Shell             10
postgresql Windows Message File            5
python     Python                     434015
python     C                          375555
python     C/C++ Header                66942
python     Bourne Shell                45091
python     MSBuild script              38910
python     m4                          15559
python     Assembly                    12298
python     make                         2953
python     HTML                         2344
python     Windows Module Definition    2081
python     Objective C                   635
python     Expect                        565
python     DOS Batch                     506
python     CSS                           328
python     Javascript                    229
python     Windows Resource File         207
python     C++                           128
python     vim script                    106
python     diff                          105
python     XML                            74
python     NAnt script                    30
python     Prolog                         24
python     Visual Basic                   12
sqlite     C                          101454
sqlite     C/C++ Header                 1546
</pre>

[](1}}})
<a name="custom_column_output"></a> []({{{1)
##  [自定义列输出 &#9650;](#___top "click to go to top of document")
Cloc的默认输出是一个有五个列的文本表:
language, file count, number of blank lines, number of comment
lines and number of code lines.  开关`--by-file`,`--3`, and `--by-percent`会产生额外的信息，但有时即使是这些信息也是不够的。.

上一节中描述的`--sql`选项提供了创建自定义输出的能力。  
本节有一对例子，展示了如何创建自定义列。
第一个例子包括一个额外的列，**Total**，它是空行、注释和代码行数之和。
第二种显示了在使用`--by-file`运行时如何包含语言名称.

**Example 1:  增加一个 "Totals"栏.**

第一步，是运行cloc并将输出保存到关系型数据库中,
SQLite in this case:
<pre>
cloc --sql 1 --sql-project x yaml-cpp-yaml-cpp-0.5.3.tar.gz | sqlite3 counts.db
</pre>
(the tar file comes from the
[YAML-C++](https://github.com/jbeder/yaml-cpp) project).

第二步，我们制作一个SQL查询，返回常规的cloc输出加上一个额外的总计列，然后将SQL语句保存到一个文`query_with_totals.sql`中:
<pre>
-- file query_with_totals.sql
select Language, count(File)   as files                       ,
                 sum(nBlank)   as blank                       ,
                 sum(nComment) as comment                     ,
                 sum(nCode)    as code                        ,
                 sum(nBlank)+sum(nComment)+sum(nCode) as Total
    from t group by Language order by code desc;
</pre>

第三，我们通过SQLite使用`counts.db`数据库运行这个查询。
我们将包含 `-header` 开关，这样SQLite就可以打印出栏目名称。

<pre>
&gt; cat query_with_totals.sql | sqlite3 -header counts.db
Language|files|blank|comment|code|Total
C++|141|12786|17359|60378|90523
C/C++ Header|110|8566|17420|51502|77488
Bourne Shell|10|6351|6779|38264|51394
m4|11|2037|260|17980|20277
Python|30|1613|2486|4602|8701
MSBuild script|11|0|0|1711|1711
CMake|7|155|285|606|1046
make|5|127|173|464|764
Markdown|2|30|0|39|69
</pre>

额外的**Total**列是存在的，但格式并不美观。
通过 `sqlite_formatter`运行输出，可以得到所需的结果:

<pre>
&gt; cat query_with_totals.sql | sqlite3 -header counts.db | sqlite_formatter
Language       files blank comment code  Total
______________ _____ _____ _______ _____ _____
C++              141 12786   17359 60378 90523
C/C++ Header     110  8566   17420 51502 77488
Bourne Shell      10  6351    6779 38264 51394
m4                11  2037     260 17980 20277
Python            30  1613    2486  4602  8701
MSBuild script    11     0       0  1711  1711
CMake              7   155     285   606  1046
make               5   127     173   464   764
Markdown           2    30       0    39    69
</pre>

The next section,
[Wrapping cloc in other scripts](#wrapping-cloc-in-other-scripts-),
显示了这些命令可以组合成一个新的实用程序的一种方法。

**Example 2: 在使用`--by-file`时包含一列"Language".**

`--by-file`的输出会省略每个文件的语言，以保存大型项目的屏幕实际文件路径可能会很长，并且“语言”列中额外包含20个左右的字符可能会过多。

作为一个例子，这里是使用与例1中相同的代码库的前几行输出结果:

<pre>
&gt; cloc --by-file yaml-cpp-yaml-cpp-0.5.3.tar.gz
github.com/AlDanial/cloc v 1.81  T=1.14 s (287.9 files/s, 221854.9 lines/s)
--------------------------------------------------------------------------------------------------------------------------------------------
File                                                                                                     blank        comment           code
--------------------------------------------------------------------------------------------------------------------------------------------
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/configure                                                        2580           2264          13691
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/configure                                                  2541           2235          13446
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/fused-src/gtest/gtest.h                                    1972           4681          13408
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/fused-src/gmock/gmock.h                                          1585           3397           9216
yaml-cpp-yaml-cpp-0.5.3/test/integration/gen_emitter_test.cpp                                              999              0           8760
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/aclocal.m4                                                        987            100           8712
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/m4/libtool.m4                                               760             65           7176
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/build-aux/ltmain.sh                                         959           1533           7169
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/fused-src/gmock-gtest-all.cc                                     1514           3539           6390
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/fused-src/gtest/gtest-all.cc                               1312           2896           5384
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/test/gtest_unittest.cc                                     1226           1091           5098
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/include/gtest/internal/gtest-param-util-generated.h         349            235           4559
</pre>

每个文件没有语言标识，这让人有些失望，但可以通过自定义的列式解决方案来弥补.

第一步，创建一个数据库，与例1中的步骤相吻合，所以我们直接进入第二步，创建所需的SQL查询。 
我们将把它存储在文件`by_file_with_language.sql`中:

<pre>
-- file by_file_with_language.sql
select File, Language, nBlank   as blank  ,
                       nComment as comment,
                       nCode    as code
    from t order by code desc;
</pre>

当我们将这个自定义的SQL查询传递给我们的数据库时，我们所需的额外列就会出现。:

<pre>
&gt; cat by_file_with_language.sql | sqlite3 -header counts.db | sqlite_formatter
File                                                                                               Language       blank comment code
__________________________________________________________________________________________________ ______________ _____ _______ _____
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/configure                                                 Bourne Shell    2580    2264 13691
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/configure                                           Bourne Shell    2541    2235 13446
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/fused-src/gtest/gtest.h                             C/C++ Header    1972    4681 13408
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/fused-src/gmock/gmock.h                                   C/C++ Header    1585    3397  9216
yaml-cpp-yaml-cpp-0.5.3/test/integration/gen_emitter_test.cpp                                      C++              999       0  8760
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/aclocal.m4                                                m4               987     100  8712
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/m4/libtool.m4                                       m4               760      65  7176
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/build-aux/ltmain.sh                                 Bourne Shell     959    1533  7169
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/fused-src/gmock-gtest-all.cc                              C++             1514    3539  6390
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/fused-src/gtest/gtest-all.cc                        C++             1312    2896  5384
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/test/gtest_unittest.cc                              C++             1226    1091  5098
yaml-cpp-yaml-cpp-0.5.3/test/gmock-1.7.0/gtest/include/gtest/internal/gtest-param-util-generated.h C/C++ Header     349     235  4559
</pre>

[](1}}})
<a name="wrapping_cloc_in_other_scripts"></a> []({{{1)
    *   [](#wrapping-cloc-in-other-scripts-)
##  [包装 cloc的其他脚本 &#9650;](#___top "click to go to top of document")

通过在脚本或程序中封装cloc，可以实现更复杂的代码计数解决方案.  
The "total lines" column from example 1 of [Custom Column Output](#custom-column-output-)
"总行数"一栏可以简化为一个命令，用这个shell脚本(在Linux上):

<pre>
#!/bin/sh
#
# These commands must be in the user's $PATH:
#   cloc
#   sqlite3
#   sqlite_formatter
#
if test $# -eq 0 ; then
    echo "Usage: $0  [cloc arguments]"
    echo "       Run cloc to count lines of code with an additional"
    echo "       output column for total lines (code+comment+blank)."
    exit
fi
DBFILE=`tempfile`
cloc --sql 1 --sql-project x $@ | sqlite3 ${DBFILE}
SQL="select Language, count(File)   as files                       ,
                      sum(nBlank)   as blank                       ,
                      sum(nComment) as comment                     ,
                      sum(nCode)    as code                        ,
                      sum(nBlank)+sum(nComment)+sum(nCode) as Total
         from t group by Language order by code desc;
"
echo ${SQL} | sqlite3 -header ${DBFILE} | sqlite_formatter
rm ${DBFILE}
</pre>

保存上面的line命令 to ``total_columns.sh`` 赋予执行权限 (``chmod +x total_columns.sh``) 
可以让我们使用如下:
<pre>
./total_columns.sh yaml-cpp-yaml-cpp-0.5.3.tar.gz
</pre>
直接得到
<pre>
Language       files blank comment code  Total
______________ _____ _____ _______ _____ _____
C++              141 12786   17359 60378 90523
C/C++ Header     110  8566   17420 51502 77488
Bourne Shell      10  6351    6779 38264 51394
m4                11  2037     260 17980 20277
Python            30  1613    2486  4602  8701
MSBuild script    11     0       0  1711  1711
CMake              7   155     285   606  1046
make               5   127     173   464   764
Markdown           2    30       0    39    69
</pre>

其他例子:
* 计算来自网络托管的特定分支的git仓库代码, 并将结果以.csv电子邮件附件的形式发送:
https://github.com/dannyloweatx/checkmarx


[](1}}})
<a name="git_and_UTF8_pathnames"></a> []({{{1)
##  [git和UTF8路径名 &#9650;](#___top "click to go to top of document")

cloc的`--git`选项可能会失败，如果你使用UTF-8字符的目录或文件名，则可能会失败(for example, see
<a href=https://github.com/AlDanial/cloc/issues/457>issue 457</a>).
解决方案,
https://stackoverflow.com/questions/22827239/how-to-make-git-properly-display-utf-8-encoded-pathnames-in-the-console-window,
是应用这个git配置命令:

<pre>
git config --global core.quotepath off
</pre>

你的控制台的字体需要能够显示Unicode字符.

[](1}}})
<a name="scale_factors"></a> []({{{1)
##  [第三代语言量表因子 &#9650;](#___top "click to go to top of document")

cloc版本在1.50之前的默认情况下，对所提供的输入，计算出了在假设的第三代计算机语言中写同样的代码需要多少行代码的粗略估计.
要产生这种输出，现在必须使用`--3`开关.

比例系数来自于2006年版的语文资产负债率，该网站上的语文资产负债率是由迈斯咨询公司网站上列出的2006年版语文资产负债率,
[http://softwareestimator.com/IndustryData2.htm](http://softwareestimator.com/IndustryData2.htm), 用这个方程:

cloc scale factor for language X = 3rd generation default gearing ratio / language X gearing ratio

For example, 
cloc 3rd generation scale factor for DOS Batch = 80 / 128 = 0.625.

这种方法最大的缺陷是，这种方法的最大缺陷是，齿轮比是针对逻辑行的源代码定义的，而不是针对物理行（coc计算）.
cloc的'scale' and '3rd gen. equiv.' 栏中的数值应以较高的标准来看待.

[](1}}})
<a name="complex_regex_recursion"></a> []({{{1)
##  [复杂正则子表达式递归极限 &#9650;](#___top "click to go to top of document")
cloc relies on the Regexp::Common module's regular expressions to remove
comments from source code.  If comments are malformed, for example the
``/*`` start comment marker appears in a C program without a corresponding ``*/``
marker, the regular expression engine could enter a recursive
loop, eventually triggering the warning
``Complex regular subexpression recursion limit``.

The most common cause for this warning is the existence of comment markers
in string literals.  While language compilers and interpreters are smart
enough to recognize that ``"/*"`` (for example) is a string and not a comment,
cloc is fooled.  File path globs, as in this line of JavaScript
<pre>var paths = globArray("**/*.js", {cwd: srcPath});
</pre>
are frequent culprits.

In an attempt to overcome this problem, a different
algorithm which removes comment markers in strings can be enabled
with the ``--strip-str-comments`` switch.  Doing so, however,
has drawbacks:  cloc
will run more slowly and the output of ``--strip-comments``
will contain strings that no longer match the input source.

[](1}}})
<a name="Limitations"></a> []({{{1)
##   [限制 &#9650;](#___top "click to go to top of document")
识别源代码中的注释比想象中的要棘手得多.
许多语言需要一个完整的解析器才能被正确计算.
cloc并没有试图解析它所要计算的任何语言，因此它是一个不完美的工具.
以下是已知的问题:

<ol>
<li>  包含源码和注释的行都算作代码行。.
</li>
<li>  字符串内的注释标记或
<a href="http://www.faqs.org/docs/abs/HTML/here-docs.html">here-documents</a>
被视为实际的注释标记，而不是字符串字形.

例如下面这几行C语言代码
<pre>printf(" /* ");
for (i = 0; i < 100; i++) {
    a += i;
}
printf(" */ ");
</pre>
look to cloc 这样:
<pre>printf(" xxxxxxx
xxxxxxx
xxxxxxx
xxxxxxx
xxxxxxx     ");
</pre>
where `xxxxxxx` represents cloc's view of commented text.
Therefore cloc counts the five lines as two lines of C code and three
lines of comments (lines with both code and comment are counted as code).

如果你怀疑你的代码中有这样的字符串, use the switch
``--strip-str-comments`` 切换到删除内嵌注释标记的算法.  
它的使用将使上述五行变成
<pre>printf("  ");
for (i = 0; i < 100; i++) {
    a += i;
}
printf("  ");
</pre>
并因此返回一个五行代码的计数。
请看下面的
[上一章节](#complex-regular-subexpression-recursion-limit-)
弊端 ``--strip-str-comments``.
</li>
<li> 嵌入语言不被识别。 例如，一个包含JavaScript的HTML文件将被完全计算为HTML.
</li>
<li> Python docstrings 可以有多种用途。 
     它们可以包含文档，注释代码块，也可以是正则字符串 (当它们出现在赋值的右侧或作为函数参数出现时)。
     cloc 无法通过上下文推断 docstrings 的含义；默认情况下，cloc 将所有 docstrings 作为注释处理.  
     The switch ``--docstring-as--code``
treats all docstrings as code.
</li>
<li> 读取语言定义文件 <tt>--read-lang-def</tt> or
<tt>--force-lang-def</tt> must be plain ASCII text files.
</li>
<li> cloc处理编译器的pragma，例如 <tt>#if</tt> / <tt>#endif</tt>, 作为代码，即使这些代码被用来阻止源码被编译，也是如此;
堵塞的行数仍然会影响到代码的数量.
</li>
</ol>

[](1}}})
<a name="AdditionalLanguages"></a> []({{{1)
#   [请求对其他语言的支持 &#9650;](#___top "click to go to top of document")

如果cloc不识别你感兴趣的语言，请创建一个 [GitHub issue](https://github.com/AlDanial/cloc/issues)
请求支持你的语言.  包括这些信息:
<ol>
<li>与该语言相关的文件扩展名。 如果语言不依赖文件扩展名，而是使用固定的文件名或`#!`风格的程序调用，请说明这些文件是什么。</li>
<li> 关于评论的定义方法的说明。</li>
<li>示例代码的链接。</li>
</ol>

[](1}}})
<a name="reporting_problems"></a> []({{{1)
#  [报告问题 &#9650;](#___top "click to go to top of document")

如果你在使用cloc时遇到问题，首先检查一下你是否有运行最新版本的工具:
<pre>
  cloc --version
</pre>
If the version is older than the most recent release
at https://github.com/AlDanial/cloc/releases, download the
latest version and see if it solves your problem.

If the problem happens with the latest release, submit
a new issue at https://github.com/AlDanial/cloc/issues *only*
if you can supply enough information for anyone reading the
issue report to reproduce the problem.
That means providing
<ol>
<li> the operating system you're running on</li>
<li> the cloc command with all options</li>
<li> the code you are counting (URL to a public git repo or zip file or
tar file, et cetera)</li>
</ol>
最后一项一般是有问题的.  
如果代码库是专有的，或者代码库的数量超过了几十千字节.
你需要尝试重构类似的输入，或者用现有的公共代码库来证明问题.

无法复制的问题报告将被忽略并最终关闭.

[](1}}})
<a name="Acknowledgments"></a> []({{{1)
##  [致谢 &#9650;](#___top "click to go to top of document")
[Wolfram Rösler](https://github.com/wolframroesler) 在测试套件中提供了大部分的代码示例.
这些例子来自于他的 [Hello World collection](http://helloworldcollection.de/).

Ismet Kursunoglu发现了MUMPS计数器的错误，并提供了一台有大量MUMPS代码的计算机来测试CLOC。.

Tod Huggins gave helpful suggestions for the Visual Basic filters.

Anton Demichev found a flaw with the JSP counter in cloc v0.76
and wrote the XML output generator for the `--xml` option.

Reuben Thomas pointed out that ISO C99 allows `//` as a comment
marker, provided code for the `--no3` and `--stdin-name`
options, counting the m4 language,
and suggested several user-interface enhancements.

Michael Bello provided code for the `--opt-match-f`,
`--opt-not-match-f`,
`--opt-match-d`, and `--opt-not-match-d`
options.

Mahboob Hussain inspired the `--original-dir` and
`--skip-uniqueness` options, found a
bug in the duplicate file detection logic and improved the JSP filter.

Randy Sharo found and fixed an uninitialized variable bug for shell
scripts having only one line.

Steven Baker found and fixed a problem with the YAML output generator.

Greg Toth provided code to improve blank line detection in COBOL.

Joel Oliveira provided code to let `--exclude-list-file` handle
directory name exclusion.

Blazej Kroll provided code to produce an XSLT file, `cloc-diff.xsl`,
when producing XML output for the `--diff` option.

Denis Silakov enhanced the code which generates `cloc.xsl` when
using `--by-file` and `--by-file-by-lang` options, and
provided an XSL file that works with `--diff` output.

Andy (awalshe@sf.net) provided code to fix several bugs:
correct output of `--counted`
so that only files that are used in the code count appear and
that results are shown by language rather than file name;
allow `--diff` output from multiple runs to be summed
together with `--sum-reports`.

Jari Aalto created the initial version of `cloc.1.pod` and
maintains the Debian package for cloc.

Mikkel Christiansen (mikkels@gmail.com) provided counter definitions
for Clojure and ClojureScript.

Vera Djuraskovic from [Webhostinggeeks.com](http://webhostinggeeks.com/)
provided the
[Serbo-Croatian](http://science.webhostinggeeks.com/cloc)
translation.

Gill Ajoft of [Ajoft Softwares](http://www.ajoft.com)
provided the
[Bulgarian](http://www.ajoft.com/wpaper/aj-cloc.html)
translation.

The
[Knowledge Team](http://newknowledgez.com/)
provided the
[Slovakian](http://newknowledgez.com/cloc.html) translation.

Erik Gooven Arellano Casillas provided an update to the MXML counter to
recognize Actionscript comments.

[Gianluca Casati](http://g14n.info) created the
[cloc CPAN package](https://metacpan.org/pod/App::cloc).

Mary Stefanova provided the
[Polish](http://www.trevister.com/blog/cloc.html)
translation.

Ryan Lindeman implemented the `--by-percent` feature.

Kent C. Dodds, [@kentcdodds](https://twitter.com/kentcdodd),
created and maintains the npm package of cloc.

[Viktoria Parnak](http://kudoybook.com)
provided the
[Ukrainian](http://blog.kudoybook.com/cloc/)
translation.

Natalie Harmann provided the
[Belarussian](http://www.besteonderdelen.nl/blog/?p=5426)
translation.

Nithyal at [Healthcare Administration Portal](http://healthcareadministrationdegree.co/)
provided the
[Tamil](http://healthcareadministrationdegree.co/socialwork/aldanial-cloc/)
translation.

Patricia Motosan
provided the
[Romanian](http://www.bildelestore.dk/blog/cloc-contele-de-linii-de-cod/)
translation.

The [Garcinia Cambogia Review Team](http://www.garciniacambogiareviews.ca/)
provided the
[Arabic translation](http://www.garciniacambogiareviews.ca/translations/aldanial-cloc/).

Gajk Melikyan provided the
provided the
[Armenian translation](http://students.studybay.com/?p=34)
for http://studybay.com.

<a href="http://www.forallworld.com/cloc-grof-sornyi-kodot/">Hungarian translation</a>
courtesy of <a href="http://www.forallworld.com/">Zsolt Boros</a>.

<a href=https://github.com/stsnel>Sietse Snel</a> implemented the parallel
processing capability available with the <tt>--processes=<i>N</i></tt>
switch.

The development of cloc was partially funded by the Northrop Grumman
Corporation.

[](1}}})
<a name="Copyright"></a> []({{{1)
##   [版权声明 &#9650;](#___top "click to go to top of document")
Copyright (c) 2006-2018, [Al Danial](https://github.com/AlDanial)
[](1}}})
