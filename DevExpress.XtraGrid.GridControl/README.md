# Grid 用法总结

**1.**屏蔽Grid默认的键盘事件<br />
这里以回车事件为例:
在Grid的ProcessGridKey事件中
```
 private void gcStockAllocation_ProcessGridKey(object sender, KeyEventArgs e)
  {
      GridControl grid = sender as GridControl;
      GridKeyPress(grid.MainView, e);
  }
```
以及一个自定义的方法
```
private void GridKeyPress(BaseView sender, KeyEventArgs e)
  {
      if (e.KeyData == Keys.Enter)
      {
          e.Handled = true;
          return;
      }
  }
```

**2.**删除Grid头部上的GroupBox[图片](./img/1.png)<br />
操作方式:<br />
* 1.在Grid上点击Run Designer 进入设计界面
* 2.左上角 选择 Views 视图 找到 OptionsVies
* 3.设置 ShowGroupPanel=False<br />
