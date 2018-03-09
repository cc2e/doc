```Java
命令模式
// ----

public class Tv {
　　public int currentChannel = 0;

　　public void turnOn() {
      // 接收开机
　　   System.out.println("The televisino is on.");
　　}

　　public void turnOff() {
      // 接收关机
　　   System.out.println("The television is off.");
　　}

　　public void changeChannel(int channel) {
      // 换频道
　　   this.currentChannel = channel;
　　   System.out.println("Now TV channel is " + channel);
　　}
}





//执行命令的接口
public interface Command {
　　void execute();
}

//开机命令
public class CommandOn implements Command {
　　private Tv myTv;

　　public CommandOn(Tv tv) {
　　   myTv = tv;
　　}

　　public void execute() {
　　   myTv.turnOn();
　　}
}

//关机命令
public class CommandOff implements Command {
　　private Tv myTv;

　　public CommandOff(Tv tv) {
　　   myTv = tv;
　　}

　　public void execute() {
　　   myTv.turnOff();
　　}
}

//频道切换命令
public class CommandChange implements Command {
　　private Tv myTv;

　　private int channel;

　　public CommandChange(Tv tv, int channel) {
　　   myTv = tv;
 　　  this.channel = channel;
　　}

　　public void execute() {
　　   myTv.changeChannel(channel);
　　}
}





//可以看作是遥控器吧
public class Control {
　　private Command onCommand, offCommand, changeChannel;

　　public Control(Command on, Command off, Command channel) {
 　　  onCommand = on;
 　　  offCommand = off;
　　   changeChannel = channel;
　　}

　　public void turnOn() {
　　   onCommand.execute();
　　}

　　public void turnOff() {
　　   offCommand.execute();
　　}

　　public void changeChannel() {
 　　  changeChannel.execute();
　　}
}

 //测试类
public class Client {
　　public static void main(String[] args) {
  　　 // 命令接收者
 　　  Tv myTv = new Tv();
 　　  // 开机命令
  　　 CommandOn on = new CommandOn(myTv);
  　　 // 关机命令
  　　 CommandOff off = new CommandOff(myTv);
  　　 // 频道切换命令
 　　  CommandChange channel = new CommandChange(myTv, 2);
 　　  // 命令控制对象
　　   Control control = new Control(on, off, channel);

  　　 // 开机
  　　 control.turnOn();
 　　  // 切换频道
 　　  control.changeChannel();
 　　  // 关机
 　　  control.turnOff();
　　}
}
   

```

