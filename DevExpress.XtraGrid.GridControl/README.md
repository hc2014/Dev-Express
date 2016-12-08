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

**2.**删除Grid头部上的GroupBox![](./img/1.png)中写着"Drag Column Header..."的地方<br />
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


**4.**绘制单元格颜色<br />
在View的CustomDrawCell时间中<br />
```
private void gvTradeList_CustomDrawCell(object sender, DevExpress.XtraGrid.Views.Base.RowCellCustomDrawEventArgs e)
  {
   if (gvTradeList.GetDataRow(e.RowHandle)["IsFreeze"].ToString() == "True")
   {
     //如果这里不去判断列名称的话即不去判断e.Column.Name，那么就是设置整行的颜色
     e.Appearance.ForeColor = Color.White;
   }
  }
```

绘制单元格颜色跟下面的设置行颜色，本质的区别在于绘制是在Grid加载的时候执行的，所以只执行一次，但是下面的RowStyle方法是一直在<br />
循环执行的,所以在程序执行的过程中Grid绑定的数据改变了,行颜色也会发生变化

**5.**设置行颜色<br />
在View的RowStyle事件中<br />
```
 private void gvTradeList_RowStyle(object sender, DevExpress.XtraGrid.Views.Grid.RowStyleEventArgs e)
  {
   DataRow dr = gvTradeList.GetDataRow(e.RowHandle);
   if (dr == null)
    {
       return;
    }
    if (bool.Parse(dr["IsFreeze"].ToString())==True)
    {
        e.Appearance.ForeColor = Color.Magenta;
    }
  }
```

**6.**行双击事件<br />
行双击事件的话,如果点击在Grid的空白地方也是会触发该事件的,所以要做一些处理
```
 private void gvTradeList_DoubleClick(object sender, EventArgs e)
  {
    MouseEventArgs arg = e as MouseEventArgs;
    if (arg == null)
    {
        return;
    }
    DevExpress.XtraGrid.Views.Grid.ViewInfo.GridHitInfo hInfo = gvTradeList.CalcHitInfo(new Point(arg.X, arg.Y));
    //判断是否左键双击
    if (arg.Button == MouseButtons.Left)
    {
        //判断光标是否在行内、判断光标是否在列内
        if (hInfo.InRow && hInfo.Column != null)
        {
         //DoSomeThing
        }
    }
  }
```

**7.**修改grid的tooltip<br />
先看效果![](./img/4.png),要实现这一的效果就需要自定tooltip,图中把0.55的折扣率显示成五五折,这一个功能的实现方式，在这里一并说了！！！<br /><br/>
首先.在工具栏找到 **ToolTipController**控件 放到界面中去名字为**MainGvTool**,然后设置**GridControl**的属性ToolTipController=MainGvTool.
![](./img/3.png)![](./img/5.png)<br /><br />
然后.在**MainGvTool**控件的**GetActiveObjectInfo**事件里面

```

```
