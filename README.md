# How to manage cell editing and submission When enabling checkbox column in Flutter DataTable (SfDataGrid)?

In this article, we will show you how to manage cell editing and submission When enabling checkbox column in [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) widget with all required properties. To enable the checkbox column, set the [showCheckboxColumn](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid/showCheckboxColumn.html) property to true at the sample level. In SfDataGrid, the checkbox column is always added as the first column. If the showCheckboxColumn is enabled, we need to resolve the column index in [onCellSubmit](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/onCellSubmit.html) at the sample level. This ensures that you can perform editing and submit the new cell value to the correct cell on the [DataGridRow](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridRow-class.html).

```dart
class EmployeeDataSource extends DataGridSource {

….
  
// To check whether the checkbox column is enabled.
  bool showCheckboxColumn = true;

@override
  Future<void> onCellSubmit(DataGridRow dataGridRow,
      RowColumnIndex rowColumnIndex, GridColumn column) async {
    final dynamic oldValue = dataGridRow
            .getCells()
            .firstWhereOrNull((DataGridCell dataGridCell) =>
                dataGridCell.columnName == column.columnName)
            ?.value ??
        '';

    final int dataRowIndex = _employeeData.indexOf(dataGridRow);

    if (newCellValue == null || oldValue == newCellValue) {
      return;
    }

    // Resolve the RowColumnIndex when showCheckboxColumn is true.
    if (showCheckboxColumn) {
      rowColumnIndex = RowColumnIndex(
          rowColumnIndex.rowIndex, rowColumnIndex.columnIndex - 1);
    }

    if (column.columnName == 'ID') {
      _employeeData[dataRowIndex].getCells()[rowColumnIndex.columnIndex] =
          DataGridCell<int>(columnName: 'ID', value: newCellValue);
      employees[dataRowIndex].id = newCellValue;
    } else if (column.columnName == 'Name') {
      _employeeData[dataRowIndex].getCells()[rowColumnIndex.columnIndex] =
          DataGridCell<String>(columnName: 'Name', value: newCellValue);
      employees[dataRowIndex].name = newCellValue.toString();
    } else if (column.columnName == 'Designation') {
      _employeeData[dataRowIndex].getCells()[rowColumnIndex.columnIndex] =
          DataGridCell<String>(columnName: 'Designation', value: newCellValue);
      employees[dataRowIndex].designation = newCellValue.toString();
    } else if (column.columnName == 'Salary') {
      _employeeData[dataRowIndex].getCells()[rowColumnIndex.columnIndex] =
          DataGridCell<int>(columnName: 'Salary', value: newCellValue);
      employees[dataRowIndex].salary = newCellValue;
    } else if (column.columnName == 'Country') {
      _employeeData[dataRowIndex].getCells()[rowColumnIndex.columnIndex] =
          DataGridCell<String>(columnName: 'Country', value: newCellValue);
      employees[dataRowIndex].country = newCellValue.toString();
    }
  }
}
```

You can download the example from [GitHub](https://github.com/SyncfusionExamples/How-to-manage-cell-editing-When-enabling-checkbox-in-Flutter-DataTable).