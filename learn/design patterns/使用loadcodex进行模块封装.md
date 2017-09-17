以下有4个文件组成
main
p1
p2
event


main.aardio
主模块使用loadcodex运行加载event模块

    import win.ui;
    /*DSG{{*/
    mainForm = win.form(text="aardio form";right=719;bottom=407)
    mainForm.add(
    tab={cls="tab";left=56;top=40;right=680;bottom=344;edge=1;z=1}
    )
    /*}}*/

    loadcodex("\res\common\event.aardio");

    mainForm.tab.loadForm("\res\p1.aardio");
    mainForm.tab.loadForm("\res\p2.aardio");    
       
    mainForm.show();

    return win.loopMessage();         

event模块 封装常用事件函数
\res\common\event.aardio  :

    import win

    showAmsg=function(msg){
    	win.msgbox(msg);
    }

    showBmsg=function(msg){
    	win.msgbox(msg);
    }


P1模块 调用 event模块定义的两个函数 \res\p1.aardio
    *猜测*
    我猜测event模块由于在主函数已经被加载到了内存中作为全局函数,
    因此P1 P2直接可以调用showAmsg/showBmsg

    import win.ui;
    /*DSG{{*/
    var p1 = win.form(text="aardio form";right=759;bottom=469;mode="child";parent=...)
    p1.add(
    button={cls="button";text="button";left=248;top=8;right=352;bottom=40;z=1};
    )
    /*}}*/

    p1.button.oncommand = function(id,event){   
        showAmsg("11111")       
    }

    p1.enableDpiScaling();
    p1.show();

    win.loopMessage();
    return p1;

P2 模块 和P1模块类似 \res\p2.aardio

    import win.ui;
    /*DSG{{*/
    var p2 = win.form(text="aardio form";right=759;bottom=469;mode="child";parent=...)
    p2.add(
    button={cls="button";text="button";left=176;top=168;right=296;bottom=208;z=1};
    edit={cls="edit";text="edit";left=160;top=48;right=320;bottom=80;edge=1;z=2}
    )
    /*}}*/

    p2.button.oncommand = function(id,event){
        showBmsg("222222222")    
    }

    p2.enableDpiScaling();
    p2.show();

    win.loopMessage();
    return p2;
