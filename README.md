<h1>MANGO LEAF DISEASE DETECTION</h1>
<p>This project uses <i><b>ResNet50</b></i> with <i><b>transfer learning</b></i>to classify 8 types of mango leaf diseases from images, including <i><b>Anthracnose, Bacterial Canker, Cutting Weevil, Die Back, Gall Midge, Healthy, Powdery Mildew, and Sooty Mould</b></i>. The dataset was carefully cleaned, resized, and balanced before training, and the model was fine-tuned to achieve high accuracy. Performance was evaluated using <i><b>accuracy, loss , confusion matrix, and classification report</b></i>, while <i><b>LIME</b></i> was used for explainability to highlight the regions of leaf images that influenced the model’s predictions, making it both accurate and interpretable for real-world agricultural applications.</p>
<h2>Data Sample</h2>
<img width="4770" height="963" alt="one_image_per_class" src="https://github.com/user-attachments/assets/bd145148-d3d8-4af4-a381-2d5b7e3e0197" />
<h2>Dataset</h2>
<p>
  <a href="https://www.kaggle.com/datasets/salehrafi/leaf-disease-dataset-mango-rice-wheat" target="_blank">
  Leaf Disease Dataset (Kaggle)
  </a>
</p>
<h2>Data Processing</h2>
<table>
  <tr><td>Image Size</td><td>224 x 224</td></tr>
</table>
<h2>Data Augmentation Parameters</h2>
<table border="1" cellpadding="8" cellspacing="0">
  <tr>
    <th>Parameter</th>
    <th>Value</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>Rescale</td>
    <td>1./255</td>
    <td>Normalize pixel values to range [0,1]</td>
  </tr>
  <tr>
    <td>Rotation Range</td>
    <td>20</td>
    <td>Random rotation up to 20 degrees</td>
  </tr>
  <tr>
    <td>Width Shift Range</td>
    <td>0.1</td>
    <td>Horizontal shift up to 10%</td>
  </tr>
  <tr>
    <td>Height Shift Range</td>
    <td>0.1</td>
    <td>Vertical shift up to 10%</td>
  </tr>
  <tr>
    <td>Shear Range</td>
    <td>0.1</td>
    <td>Shear transformation</td>
  </tr>
  <tr>
    <td>Zoom Range</td>
    <td>0.1</td>
    <td>Random zoom up to 10%</td>
  </tr>
  <tr>
    <td>Horizontal Flip</td>
    <td>True</td>
    <td>Randomly flip images horizontally</td>
  </tr>
</table>
<h2>Data Split</h2>
<table>
  <tr>
    <th>Training</th>
    <th>Validation</th>
    <th>Evaluation</th>
  </tr>
  <tr>
    <td>3200</td>
    <td>400</td>
    <td>400</td>
  </tr>
</table>

<h2>Class Weights</h2>
<table>
  <tr>
    <th>Class Name</th>
    <th>Weight</th>
  </tr>
  <tr><td>Anthracnose</td><td>1.0</td></tr>
  <tr><td>Bacterial Canker</td><td>1.0</td></tr>
  <tr><td>Cutting Weevil</td><td>1.0</td></tr>
  <tr><td>Die Back</td><td>1.0</td></tr>
  <tr><td>Gall Midge</td><td>1.0</td></tr>
  <tr><td>Healthy</td><td>1.0</td></tr>
  <tr><td>Powdery Mildew</td><td>1.0</td></tr>
  <tr><td>Sooty Mould</td><td>1.0</td></tr>
</table>
<h2>Base Model: ResNet50 – Unfrozen Layers</h2>

<table>
  <thead>
    <tr>
      <th>Stage</th>
      <th>Layers Unfrozen</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Conv1</td>
      <td><code>conv1</code></td>
    </tr>
    <tr>
      <td>Conv2 Block 1</td>
      <td><code>conv2_block1_1</code>, <code>conv2_block1_2</code></td>
    </tr>
    <tr>
      <td>Conv2 Block 2</td>
      <td><code>conv2_block2_1</code>, <code>conv2_block2_2</code></td>
    </tr>
    <tr>
      <td>Conv2 Block 3</td>
      <td><code>conv2_block3_1</code>, <code>conv2_block3_2</code></td>
    </tr>
    <tr>
      <td>Conv3 Block 1</td>
      <td><code>conv3_block1_1</code>, <code>conv3_block1_2</code></td>
    </tr>
    <tr>
      <td>Conv3 Block 2</td>
      <td><code>conv3_block2_1</code>, <code>conv3_block2_2</code></td>
    </tr>
    <tr>
      <td>Conv3 Block 3</td>
      <td><code>conv3_block3_1</code>, <code>conv3_block3_2</code></td>
    </tr>
    <tr>
      <td>Conv3 Block 4</td>
      <td><code>conv3_block4_1</code>, <code>conv3_block4_2</code></td>
    </tr>
  </tbody>
</table>

<h2>Model Summary</h2>

<table>
  <thead>
    <tr>
      <th>Layer (type)</th>
      <th>Output Shape</th>
      <th>Param #</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>resnet50 (Functional)</td>
      <td>(None, 7, 7, 2048)</td>
      <td>23,587,712</td>
    </tr>
    <tr>
      <td>global_average_pooling2d (GlobalAveragePooling2D)</td>
      <td>(None, 2048)</td>
      <td>0</td>
    </tr>
    <tr>
      <td>dense (Dense)</td>
      <td>(None, 2048)</td>
      <td>4,196,352</td>
    </tr>
    <tr>
      <td>dropout (Dropout)</td>
      <td>(None, 2048)</td>
      <td>0</td>
    </tr>
    <tr>
      <td>dense_1 (Dense)</td>
      <td>(None, 8)</td>
      <td>16,392</td>
    </tr>
  </tbody>
</table>

<p><strong>Total params:</strong> 27,800,456 (106.05 MB)<br>
<strong>Trainable params:</strong> 5,193,224 (19.81 MB)<br>
<strong>Non-trainable params:</strong> 22,607,232 (86.24 MB)</p>
<p>
  <a href="https://drive.google.com/file/d/1b0DBPEeRs2qR2TIxXXXM1Df1Mg6epT-o/view?usp=sharing" target="_blank">
    Download Model
  </a>
</p>
<h2>Train & Validation Acc and Loss</h2>
<table>
  <tr>
   <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/accuracy_plot.png" /></td>
    <td><img  src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/loss_plot.png" /></td>
  </tr>
</table>
<h2>Classification Report & Confussion Matrix</h2>
<table>
  <tr>
   <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/classification_report_heatmap.png" /></td>
    <td><img  src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/confusion_matrix_blue.png" /></td>
  </tr>
</table>
<h2>Lime Analysis</h2>
<table>
  <tr>
    <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/Anthracnose.png"/></td>
    <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/Bacterial%20Canker.png"/></td>
    <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/Cutting%20Weevil.png"/></td>
    <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/Die%20Back.png"/></td>
  </tr>
  <tr>
    <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/Gall%20Midge.png"/></td>
    <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/Healthy.png"/></td>
    <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/Powdery%20Mildew.png"/></td>
    <td><img src="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/Plots/Sooty%20Mould.png"/></td>
  </tr>
</table>
<h2>Author & License</h2>
<p><strong>Author:</strong>
<a href="https://www.linkedin.com/in/smnahmed28/" target="_blank">
    S. M. Nihal Ahmed
  </a>
</p>
<p><strong>License:</strong> 
  <a href="https://github.com/nihal4/Mango_leaf_Disease_Detection_ResNet50/blob/main/LICENSE" target="_blank">
    MIT License
  </a>
</p>
