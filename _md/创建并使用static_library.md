##[iOS开发]创建并使用static library
在进行iOS开发时，底层的很多功能代码都是采用C/C++来实现的，并且与APP的code有层次上的区别，切这部分功能代码是可以重用的，这个时候我们期望把这部分代码放在单独的library中。
在iOS上，是没有办法使用dynamic library的，所以我们需要创建一个static library( for iOS ),具体步骤如下：  
1.XCode->File->NewProject->iOS(Category)/Framework & Library/Cocoa Touch Static Library  
![create static library project](/assets/images/posts/createStaticLibraryProject.png")  
建立好project以后，将已经存在的source file添加到project中，我以最简单的一个c file为例：  

	{% highlight c %}
	//zenLog.h  
	#ifndef __ZENLOG_H__
	#define __ZENLOG_H__

	void hello();

	#endif  
	{% endhighlight %}
实现

	{% highlight c %}
	//zenLog.c
	#include <stdio.h>
	#include "zenLog.h"

	void hello() {
		printf( "Hello, World!" );
	}
	{% endhighlight %}
将这两个文件添加到project中以后  
![add source files](/assets/images/posts/addLibrarySourceFiles.png)  
直接进行compile，注意这个时候要把active scheme选择正确**for iOS device or iOS Simulator**（与后面要reference此lib 的APP project active scheme匹配，否则会出现此libary在APP project中无法正常加载的问题），此外，要注意需要debug还是release版本。编译完成以后，可以在Products group中选择对应的library，然后右键“Show in Finder”，这样为后续在APP project中添加引用做好准备。
  
2.创建一个APP project，把在finder中显示的static library直接drag & drop到APP project的“Frameworks group”中  
![add library](/assets/images/posts/addLibrary.png)    
这样XCode会自动帮我们在Build Phases->Link Binaray with Libraries中把reference的static library添加上。  
![link reference added](/assets/images/posts/linkReferenceAdded.png)  

3.在viewController.m的viewDidLoad中添加

	{% highlight objc %}
	-(void)viewDidLoad {
		[ super viewDidLoad ];
		hello();
	}
	{% endhighlight %}  
4.compile & run; "**Hello, World!**"就会在XCode的output窗口显示出来。  
![output](/assets/images/posts/output.png)  
	
