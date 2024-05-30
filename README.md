The task is to write an application to demonstrate the operation of algorithms for drawing segments and polygons. The following examples were chosen as examples for implementation algorithms: Cohen-Sutherland algorithm and convex polygon clipping algorithm. C# and the WPF framework were chosen as the programming language.
<br>
### Code examples:
<br>
An example of the implementation of the main window class constructor, where a coordinate system is created for displaying lines and polygons. The ScottPlot library is used to build various graphical objects.
<br>

``` cs
public MainWindow()
{
    InitializeComponent();
    System.Drawing.Color color = ColorTranslator.FromHtml("#1f24c7");
    Plot.Plot.XAxis.Label("X", color);
    Plot.Plot.YAxis.Label("Y", color);
}
```
<br>
<br>
Below is the implementation of the polynomial clipping algorithm:
<br>

``` cs
private void PolynomCutAlghoritm(int polynom_size, double[][] poly_area, double[][] clip_area)
{
    for (int i = 0; i < 4; i++)
    {
        int k = (i + 1) % 4;
        clip(poly_area, clip_area[i][0], clip_area[i][1], clip_area[k][0], clip_area[k][1], ref polynom_size);
    }
    Plot.Plot.Clear();
    coordinates.Clear();
    int a = 0; 
    while (a != polynom_size)
    {
        coordinates.Add(poly_area[a][0]);
        coordinates.Add(poly_area[a][1]);
        a++;
    }
    coordinates.Add(poly_area[0][0]);
    coordinates.Add(poly_area[0][1]);
    ReDrawPlot();
    DrawRectangle(this.x_max, this.y_max, this.x_min, this.y_min)
}
```
<br>
Below is an implementation of the Cohen-Sutherland algorithm:
<br>

``` cs
private void CohenSutherlandAlghoritm(double x1, double y1, double x2, double y2)
{
    int code1 = ComputeCode(x1, y1);
    int code2 = ComputeCode(x2, y2)
    bool accept = false
    while (true)
    {
        if ((code1 == 0) && (code2 == 0))
        {
            accept = true;
            break;
        }
        else if (Convert.ToBoolean(code1 & code2))
        {
            break;
        }
        else
        {
            int code_out;
            double x = 0, y = 0
            if (code1 != 0)
            {
                code_out = code1;
            }
            else
            {
                code_out = code2;

            if (Convert.ToBoolean(code_out & TOP))
            {
                x = x1 + (x2 - x1) * (y_max - y1) / (y2 - y1);
                y = y_max;
            }
            else if (Convert.ToBoolean(code_out & BOTTOM))
            {
                x = x1 + (x2 - x1) * (y_min - y1) / (y2 - y1);
                y = y_min;
            }
            else if (Convert.ToBoolean(code_out & RIGHT))
            {
                y = y1 + (y2 - y1) * (x_max - x1) / (x2 - x1);
                x = x_max;
            }
            else if (Convert.ToBoolean(code_out & LEFT))
            {
                y = y1 + (y2 - y1) * (x_min - x1) / (x2 - x1);
                x = x_min;

            if (code_out == code1)
            {
                x1 = x;
                y1 = y;
                code1 = ComputeCode(x1, y1);
            }
            else
            {
                x2 = x;
                y2 = y;
                code2 = ComputeCode(x2, y2);
            }
        }
    }
    if (accept)
    {
        DrawLine(x1, y1, x2, y2);
        Item item = new Item();
        item.x1 = x1.ToString();
        item.y1 = y1.ToString();
        item.x2 = x2.ToString();
        item.y2 = y2.ToString();
        table.Items.Add(item);
    }

    }
    }
}
```
<br>
<br>
<br>
Several methods are also presented to handle the choice of clipping algorithm:
<br>

``` cs
private void line_radio_btn_Checked(object sender, RoutedEventArgs e)
 {
     if (add_line_btn.Content.ToString() == "Add point")
     {
         add_line_btn.Content = "Add line";
     }
     add_line_btn.IsEnabled = true;
     show_btn.IsEnabled = true;
     remove_btn.IsEnabled = true;
     cut_btn.IsEnabled = true;
     x1_word.Visibility = Visibility.Visible;
     x2_word.Visibility = Visibility.Visible;
     y1_word.Visibility = Visibility.Visible;
     y2_word.Visibility = Visibility.Visible;
     text_block_x1.Visibility = Visibility.Visible;
     text_block_x2.Visibility = Visibility.Visible;
     text_block_y1.Visibility = Visibility.Visible;
     text_block_y2.Visibility = Visibility.Visible;
     x1_word.Text = "X1:";
     x2_word.Text = "X2:";
     y1_word.Text = "Y1:";
     y2_word.Text = "Y2:";
     table.Items.Clear();
     Plot.Plot.Clear();
     if (table.Columns.Count != 4)
     {
         DataGridTextColumn coloumn1 = new DataGridTextColumn { Header = "x2" };
         DataGridTextColumn coloumn2 = new DataGridTextColumn { Header = "y2" };
         Binding binding1 = new Binding("x2");
         Binding binding2 = new Binding("y2");
         coloumn1.Binding = binding1;
         coloumn2.Binding = binding2;
         DataGridLength length = new DataGridLength(147.7d);
         coloumn1.Width = length;
         coloumn2.Width = length;
         table.Columns[0].Width = length;
         table.Columns[1].Width = length;
         table.Columns.Insert(1, coloumn1);
         table.Columns.Insert(3, coloumn2);
         table.CanUserResizeColumns = false;
     }
     coordinates.Clear();
 
 private void polygon_radio_btn_Checked(object sender, RoutedEventArgs e)
 {
     add_line_btn.Content = "Add point";
     add_line_btn.IsEnabled = true;
     show_btn.IsEnabled = true;
     remove_btn.IsEnabled = true;
     cut_btn.IsEnabled = true;
     x1_word.Visibility = Visibility.Visible;
     x2_word.Visibility = Visibility.Hidden;
     y1_word.Visibility = Visibility.Visible;
     y2_word.Visibility = Visibility.Hidden;
     text_block_x1.Visibility = Visibility.Visible;
     text_block_x2.Visibility = Visibility.Hidden;
     text_block_y1.Visibility = Visibility.Visible;
     text_block_y2.Visibility = Visibility.Hidden;
     text_block_x1.Text = String.Empty;
     text_block_y1.Text = String.Empty;
     x1_word.Text = "X1:";
     x2_word.Text = "X2:";
     y1_word.Text = "Y1:";
     y2_word.Text = "Y2:";
     table.Items.Clear();
     Plot.Plot.Clear();
     table.Columns.Clear();
     DataGridTextColumn coloumn1 = new DataGridTextColumn { Header = "x1" };
     DataGridTextColumn coloumn2 = new DataGridTextColumn { Header = "y1" };
     Binding binding1 = new Binding("x1");
     Binding binding2 = new Binding("y1");
     coloumn1.Binding = binding1;
     coloumn2.Binding = binding2;
     DataGridLength length = new DataGridLength(295.4d);
     coloumn1.Width = length;
     coloumn2.Width = length;
     table.Columns.Add(coloumn1);
     table.Columns.Add(coloumn2);
     coordinates.Clear();
 }
}
```
<br>
The clipping region is created using a second window into which the user enters the appropriate maximum and minimum region coordinates. Information about the entered coordinates in the second window is passed to the method using a delegate that has the following declaration:
<br>

``` cs
public delegate void MyDelegate(double x_min, double x_max, double y_min, double y_max);
private void Button_Click(object sender, RoutedEventArgs e)
{
    if (text_box_max_x.Text != String.Empty && text_box_max_y.Text != String.Empty && text_box_min_x.Text != String.Empty && text_box_min_y.Text != String.Empty)
    {
        myDelegate.Invoke(double.Parse(text_box_min_x.Text), double.Parse(text_box_max_x.Text), double.Parse(text_box_min_y.Text), double.Parse(text_box_max_y.Text));
        this.Close();
    }
}
```
<br>
The result is the following application:

![](https://raw.githubusercontent.com/NikitaBeliayev/BSU-Computer-Graphic-Programming/development/Cut%20off%20algorithm/.media/Screenshot%202023-06-16%20231131.png)
![](https://raw.githubusercontent.com/NikitaBeliayev/BSU-Computer-Graphic-Programming/development/Cut%20off%20algorithm/.media/Screenshot%202023-06-16%20235344.png)
![](https://raw.githubusercontent.com/NikitaBeliayev/BSU-Computer-Graphic-Programming/development/Cut%20off%20algorithm/.media/Screenshot%202023-06-16%20235435.png)
![](https://raw.githubusercontent.com/NikitaBeliayev/BSU-Computer-Graphic-Programming/development/Cut%20off%20algorithm/.media/Screenshot%202023-06-17%20000106.png)
