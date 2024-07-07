# renderdoc2fbx
renderdoc python extension for exporting fbx data

## Installation

copy `fbx_exporter` folder to `%appdata%\qrenderdoc\extensions`

If you are in the windows platform, you can use `install.bat` to install the extension.

## Feature

Export ASCII FBX File Support

+ **Vertex** 
+ **Normal** 
+ **UV**
+ **Tangent**
+ **VertexColor**

![FBX](image/01.png)

## Usage

make sure you copy the extension to the `%appdata%\qrenderdoc\extensions` directory

launch `renderdoc` and open the `Extension Manager`

![FBX](image/02.png)

then go to the Mesh Viewer click the extension icon menu to export the current data as the FBX file.

![FBX](image/03.png)

## Notice 

~~Export Large Mesh especially more than 30000 vertices need several seconds~~  
~~Python extension not efficient enough for that large Mesh. ~~

I change the export method which greatly enhance the export performance. 

## Edit by HQiuzi

Fill in the parameter name according to your form.

I change the way to find Vertex input window in line 460:

``` Python
windowlist = main_window.findChildren(QtWidgets.QTableView) #Change by your window name
table = windowlist[-1]
```
And sometimes the input list format may be wrong, please check the shape of data list in line 128:
``` Python
for i, idx in enumerate(idx_dict):
    for attr in attr_list:
        if attr == "in_ATTRIBUTE3":  # Change by your attribute name
            try:
                value = [int(item) for item in data[attr][i]]
            except:
                raise Exception(len(data[attr]))
        else:
            value = [float(data[attr][j][i]) for j in range(len(data[attr]))]
        value_dict[attr].append(value)
        if idx not in vertex_data[attr]:
            vertex_data[attr][idx] = value
```