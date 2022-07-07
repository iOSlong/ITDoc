### 大全v2.7.2 详情TableView崩溃案例保留：

#### 首先分析对应TableView崩溃代码演示：

section[0] - 专辑详情模块，变化(详细是否含有展开数据)
section[1] - 广告或其他模块，变化(insert，delete，reload)

1. TableView的数据源section[0]发生变化之后没有及时刷新TableView，此后secion[1]再调用以下组合接口导致崩溃：
        
```
[self.tableProxy reloadViewModelsAtSection:1];//刷新section[1].

- (void)reloadViewModelsAtSection:(NSUInteger)section {
    NSIndexSet *indesSet = [NSIndexSet indexSetWithIndex:section]
    [self.tableView beginUpdates];
    //insert|delete|selection|reloadSection |~ 譬如:
    [self.tableView reloadSections:indesSet withRowAnimation:UITableViewRowAnimationNone];
    [self.tableView endUpdates];
}
```
崩溃日志如下：
> exception = Invalid update: invalid number of rows in section 0.  The number of rows contained in an existing section after the update (3) must be equal to the number of rows contained in that section before the update (0), plus or minus the number of rows inserted or deleted from that section (0 inserted, 0 deleted) and plus or minus the number of rows moved into or out of that section (0 moved in, 0 moved out).

是section[1]发生变化的时候，想要刷新table的section[1]的数据，但是table对应section[0]的数据源其实已经发生了变化，并且没有对应刷新table，此时用如上组合方式只对IndexSet为section[1]的区域进行刷新会导致崩溃。

* 控件使用原则：
    1. 控件(TableView)依赖的 dataSource 发生任何变化都要及时刷新到改控件(TableView). 
    2. 刷新方法调用原则是，(TableView)刷新的区域必须涵盖对饮数据源变化的区域。


> 解决办法：

```
//1. 在section[0]发生变化的时候及时刷新table对应模块：
[self.tableProxy reloadViewModelsAtSection:0];//刷新section[0].

//2. 刷新的区域必须涵盖对饮数据源变化的区域，需要同时刷新secion[0]和section[1]
[self.tableProxy reloadViewModelsWithIndexesRange:NSMakeRange(0, 2)];
- (void)reloadViewModelsWithIndexesRange:(NSRange)range {
    NSIndexSet *indesSet = [NSIndexSet indexSetWithIndexesInRange:range];
    [self.tableView beginUpdates];
    [self.tableView reloadSections:indesSet withRowAnimation:UITableViewRowAnimationNone];
    [self.tableView endUpdates];
}
```

> 补充：

* reloadData,此方法将全盘依赖数据源刷新tableView，发生大批量界面变动时推荐使用。
* beginUpdates、endUpdates 组合调用只对它们之间涵盖的cell做数据源刷新，没涵盖的cells只有高度的重算没有数据源重绘，所以效率高一些。




#### 大全详情TableView崩溃描述
1. 详情页面中可同时显示的TableView1 与专辑简介弹框的TableView2 共用一组数据源(专辑详情)AlbumSectionViewModel
2. 通过行为控制，TableView1与tableView2 中 AlbumSectionViewModel.cellViewModels的值不一样。

3. 当专辑简介弹框弹出的时候 AlbumSectionViewModel受到TableView2控制和修改，此时如果详情界面的TableView1的数据源发生变化(广告、剧集、推荐等跟新)，需要刷新TableView1，此时没有考虑到AlbumSectionViewModel已经被TableView2修改，然后调用了前一小节中描述的方法，导致应用崩溃。


> 解决：

TableView1与tableView2各使用自己的一组数据源，从数据源上解耦得以模块独立。 能够保证TableView1的数据源变动时候刷新时，不会有别的模块对源数据的未知模块进行篡改导致错误。







