<div align="center">

## Rotating Cursor for DOS


</div>

### Description

Creates a rotating circle cursor for DOS
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Ashish\.Nagar](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/ashish-nagar.md)
**Level**          |Beginner
**User Rating**    |4.3 (13 globes from 3 users)
**Compatibility**  |C
**Category**       |[Graphics/ Sound](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/graphics-sound__3-15.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/ashish-nagar-rotating-cursor-for-dos__3-11514/archive/master.zip)

### API Declarations

```
#include&lt;stdio.h&gt;
#include&lt;conio.h&gt;
#include&lt;stdlib.h&gt;
#include&lt;dos.h&gt;
#include&lt;graphics.h&gt;
```


### Source Code

```
#include<stdio.h>
#include<conio.h>
#include<stdlib.h>
#include<dos.h>
#include<graphics.h>
main()
{
	union REGS i,o;
	int gd = DETECT,gm,maxx,maxy,x,y,button,cl=1,rad=10,flag=0;
	char name[50];
	initgraph(&gd,&gm,"\\tc\\bgi");
	maxx = getmaxx();
	maxy = getmaxy();
	restrictmouseptr(1,1,maxx,maxy);
	gotoxy(1,2);
	gotoxy(15,2);
	gotoxy(55,3);
	while(!kbhit())
	{
		getmousepos(&button,&x,&y);
		setfillstyle(1,2);
		fillellipse(x,y,10,rad);
		if(flag==0)
		 rad++;
		else
		 rad--;
		if(rad>=10)
		 flag=1;
		if(rad<=1)
		 flag=0;
		delay(30);
		cleardevice();
	}
	getch();
	return 0;
}
initmouse()
{
	union REGS i,o;
	i.x.ax = 0;
	/* sets the interrept interface */
	int86(0x33,&i,&o);
	return(o.x.ax);
}
showmouseptr()
{
	union REGS i,o;
	i.x.ax = 1;
	/* sets the interrept interface */
	int86(0x33,&i,&o);
	return 0;
}
restrictmouseptr(int x1,int y1,int x2,int y2)
{
	union REGS i,o;
	i.x.ax = 7;
	i.x.cx = x1;
	i.x.dx = x2;
	/* sets the interrept interface */
	int86(0x33,&i,&o);
	i.x.ax = 8;
	i.x.cx = y1;
	i.x.dx = y2;
	/* sets the interrept interface */
	int86(0x33,&i,&o);
	return 0;
}
getmousepos(int *button,int *x,int *y)
{
	union REGS i,o;
	i.x.ax = 3;
	/* sets the interrept interface */
	int86(0x33,&i,&o);
	*button = o.x.bx;
	*x = o.x.cx;
	*y = o.x.dx;
	return 0;
}
```

