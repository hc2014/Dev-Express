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
