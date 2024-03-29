# fsg-benchmark
## IMPORTANT! We have released the source code of FSG: [Check it here!](https://github.com/iago-suarez/FSG)

## Benchmark of the article "FSG: A statistical approach to line detection via fast segments grouping"

In IROS 2018 we presented a new approach to line detection based on the grouping of line segments. In order to test the performance of our method, we have grouped by hand which of the LSD segments in the York Urban Dataset (YUD) belongs to the same image line. That way it is possible to use these labels to evaluate any segment gouping algorithm. In this repo we make public this dataset, if you use it in your research you have to reference our paper:

> Iago Suárez, Enrique Muñoz, José M. Buenaposada, Luis Baumela. "FSG: A statistical approach to line detection via fast segments grouping". IROS 2018.


## Dataset structure
The dataset is divided in two directories:

* **YUDSegmentGroups**: This directory contains the information of the segments detected on all the Dataset images and it tells you which of those segments are aligned in the image.
* **YUDBadSegments**: This directory contains the data used in the experiment "Validation of segment clusters" where we evaluate the problem of segment grouping as a binary classification problem. 

## XML Format

The format of the XML files created for each image has the following structure:

```xml
    <image_size>640, 480</image_size>
    <image_name>P1080092.jpg</image_name>
    <segments numberOfSegments="976">
        <segment>
            <id>0</id>
            <endpoints>[70.5912, 32.9707, 66.473, 0.517393]</endpoints>
        </segment>
        <segment>
            <id>1</id>
            
            ...
            
          <endpoints>[124.033, 475.999, 128.981, 474.068]</endpoints>
        </segment>
    </segments>
    <clusters numberOfClusters="102">
        <cluster>[520, 529, 543, 567, 555, 556, 571, 570]</cluster>
        <cluster>[573, 554, 532, 444, 344]</cluster>
        
        ...
        
        <cluster>[151, 69, 228]</cluster>
    </clusters>
</segment_clustering>
```

In the `<image_size>` and `<image_name>` tags, the name and dimensions of the image are specified. The `<segments>` tag, contains the list of all the segments detected by the OpenCV implementation of LSD in the image, where each segment has its `<segment>` tag, containing the identifier `<id>` and the segment endpoints in format `<endpoints>[x1, y1, x2, y2]</endpoints>` where the first endpoint of the segment is (x1, y1) and the second one (x2, y2). Next, there is the `<clusters>` tag that contains the hand-labeled groups of aligned segments. Each group has its `<cluster>` tag and inside it a list with the identifiers of the segments that belongs to that cluster.
