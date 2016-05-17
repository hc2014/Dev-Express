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

**2.**删除Grid头部上的GroupBox[图片](./img/1.png)中写着"Drag Column Header..."的地方<br />
操作方式:<br />
* 1.在Grid上点击Run Designer 进入设计界面
* 2.左上角 选择 Views 视图 找到 OptionsView
* 3.设置 ShowGroupPanel=False<br />


**3.**Grid绑定数据后,状态列显示中文字<br />
在Grid的MainView视图中的CustomColumnDisplayText事件中<br />
```
private void gvTradeList_CustomColumnDisplayText(object sender, DevExpress.XtraGrid.Views.Base.CustomColumnDisplayTextEventArgs e)
 {
  //如果是状态列
  if (e.Column.FieldName == "ttt_TradeStatus")
   {
      //如果状态列的值是5
       if (e.DisplayText == "5")
       {
           e.DisplayText = "打单出库";
       }
   }
 }
```
