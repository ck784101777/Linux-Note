<!-- GFM-TOC -->
* [前言](#前言)
* [一、Linux的基本概念与原理性问题](#Linux的基本概念与原理性问题)
    * [1.Linux中一切皆文件](#1.Linux中一切皆文件)
# 前言

  本文主要介绍Linux的基本概念和理论，适合有一定Linux基础的读者阅读。
  

# 一、Linux的基本概念与原理性问题

## 1.Linux中一切皆文件
   linux下“一切皆文件”是Unix/Linux的基本哲学之一。
   <div align="center"> <img src="https://github.com/ck784101777/Linux-Note/blob/master/photos/1577169516(1).jpg?raw=true"/> </div><br>
   普通文件、目录、字符设备、块设备和网络设备（套接字）等在Unix/Linux都被当做文件来对待。虽然他们的类型不同，但是linux系统为它们提供了一套统一的操作接口。
   对于普通文件很好理解，难理解的是设备，我们这里拿U盘来举例，通常在Windows系统中，插入u盘。这时候就不得不提虚拟文件系统了。

   虚拟文件系统（Virtual File System，简称VFS）。linux支持多种文件系统（如vfat,ext2,ext3等），为了方便管理，在所有这些文件系统上面提供了一层抽象，即虚拟文件系统。虚拟文件系统为各类文件系统提供了统一的操作界面和应用编程接口，也就是说，不论是什么类型的文件系统，都必须提供符合VFS标准的接口。

   <div align="center"> <img src="https://github.com/ck784101777/Linux-Note/blob/master/photos/7OZ%5D6KRDTRAR%7BAITOUK@24W.png?raw=true"/> </div><br>
   
   结合上图可知，应用程序通过文件操作函数（open()、close()、read()、write()、ioctl()）调用VFS提供的系统调用函数接口(sys_open()、sys_close()、sys_read()、sys_write()、sys_ioctl())同VFS进行交互，VFS通过驱动程序提供的file_operation接口同设备驱动进行交互。

   linux下每一类设备在驱动层都定义了操作方法（例如：字符设备的操作方法为def_chr_fops，块设备为 def_blk_fops，网络设备为bad_sock_fops），并且不同类型的设备底层操作方法是不一样的，但是驱动层通过file_operations方法把不同类型设备的差异屏蔽了，这就使得VFS可以通过统一的file_operations接口来访问不同类型的设备。这就是linux能将所有设备都理解为文件的原因。


## 2.Linux内核启动过程
