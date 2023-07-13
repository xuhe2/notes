* `qlineedit`对于行的编辑
* `qlabel`QT的标签.
* `Qpushbutton`



# 显示一个表格

```cpp
#include <QApplication>

#include <QTableView>
#include <QHeaderView>
#include <QStandardItemModel>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
	
	/* 创建表格视图 */
    QTableView *tableView = new QTableView;
    
    /* 设置表格视图大小 */
    tableView->resize(850, 400);

    /* 创建数据模型 */
    QStandardItemModel* model = new QStandardItemModel();

    /* 设置表格标题行(输入数据为QStringList类型) */
    model->setHorizontalHeaderLabels({"ID", "User Name", "City", "Classify", "Score", "Sign"});

    /* 自适应所有列，让它布满空间 */
    tableView->horizontalHeader()->setSectionResizeMode(QHeaderView::Stretch);

    /* 加载共10行数据，并每行有6列数据 */
    for (int i = 0; i < 10; i++) {
        /* 加载第一列(ID)数据 */
        model->setItem(i, 0, new QStandardItem(QString("100%1").arg(i)));
        /* 加载第二列(User Name)数据 */
        model->setItem(i, 1, new QStandardItem(QString("User%1").arg(i)));
        /* 加载第三列(City)数据 */
        model->setItem(i, 2, new QStandardItem("Shanghai"));
        /* 加载第四列(Classify)数据 */
        model->setItem(i, 3, new QStandardItem("Engineer"));
        /* 加载第五列(Score)数据 */
        model->setItem(i, 4, new QStandardItem("80"));
        /* 加载第六列(Sign)数据 */
        model->setItem(i, 5, new QStandardItem("Hello world!"));
    }

    /* 设置表格视图数据 */
    tableView->setModel(model);

    /* 显示 */
    tableView->show();

    return a.exec();
}
```

