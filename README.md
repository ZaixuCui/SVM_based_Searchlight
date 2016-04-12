# SVM_based_Searchlight
Matlab code for SVM based searchlight analysis   
  
PSOM (https://github.com/PSOM) is needed to run this program.  
  
First, execute function Image_ROIs.m to construct a sphere for each voxel in the image  
Function Image_ROIs:  
Input:  
Mask_img: the path of the mask image (e.g., one of the subject’ image which will be used for searchlight analysis)  
Radium: the radium for the sphere  
Output:  
A file named ‘All_ROIs.mat’ will be generated, which contains the location of the sphere for each voxel  
To run the function Image_ROIs, Image_ROIs_Child.m, ROIs_Merge.m and gen_ROI.m are needed.  
Then, execute function Searchlight_Analysis.m to apply searchlight analysis  
  
        
Function Searchlight_Analysis:  
Searchlight_Analysis (SubjectsData_Path, SubjectsLabel, All_ROIs_Path, Img_Template, ResultantFolder)  
Input:  
SubjectsData_Path:  
.mat file with a matrix nm (n is quantity of subjects, m is quantity of features)  
Can be acquired using commands listed:  
NC_Cell = g_ls('/data/s1/cuizaixu/DATA_ShuHua_Dyslexia_NCRandom/GMV/NC/nii');  
Dyslexia_Cell = g_ls('/data/s1/cuizaixu/DATA_ShuHua_Dyslexia_NCRandom/GMV/Dyslexia/nii');  
SubjectsImg_Path = [NC_Cell; Dyslexia_Cell];  
SubjectsData = [];  
for i = 1:length(SubjectsImg_Path)  
Vref = spm_vol(SubjectsImg_Path{i});  
Data = spm_read_vols(Vref); Data = reshape(Data, 1, Vref.dim(1)Vref.dim(2)*Vref.dim(3));  
SubjectsData = [SubjectsData; Data];  
end  
save /data/s1/cuizaixu/DATA_ShuHua_Dyslexia_NCRandom/GMV/SubjectsData.mat SubjectsData;  
SubjectsLabel:  
array of -1 or 1  
All_ROIs_Path:  
The path of the file ‘All_ROIs.mat’acquired from function Image_ROIs function  
Img_Template:  
.nii format  
path of one of the subjects' image (for acquiring dimensions of subjects' images)  
  
Reference papers of searchlight analysis:  
Haynes JD, Sakai K, Rees G, Gilbert S, Frith C, Passingham RE. (2007): Reading hidden intentions in the human brain. Curr Biol 17(4):323-8.  
Kriegeskorte N, Goebel R, Bandettini P. (2006): Information-based functional brain mapping. Proc Natl Acad Sci U S A 103(10):3863-8.  
  
Copyright (c) Zaixu Cui, State Key Laboratory of Cognitive Neuroscience and Learning, Beijing Normal University.
Contact information: zaixucui@gmail.com
