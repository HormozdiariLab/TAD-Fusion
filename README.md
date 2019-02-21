################
I. Fit the model with Hi-C data
  1. Install CPLEX
  2. Set variables CPLEX_INCLUDE and CPLEX_LIB to the directory where CPLEX is installed
  3. Compile the source by running the script
        ./compile_fit_hic_model.sh
  4. If the compilation is successful, an executable file "fit_hic_model" will be generated in the folder "src"
  5. Options for fitting the model
    -fn       Data file path
    -ff       Data file format ("full_matrix_format" of Schmitt et al. data or "sparse_matrix_format" of Rao et al. data)
    -res      Hi-C matrix bin resolution (e.g. 40kb, 10kb, 5kb)
    -mn       Minimum distance (by a number of bins), any bin pair that the distance is shorter than this threshold will not be considered for fitting the model
    -mx       Maximum distance, any bin pair that the distance is longer than this threshold will not be considered for fitting the model
    -method   Method for fitting ("full" to fit the model from the whole Hi-C data at one time or "segmentation" to partition the matrix into segments and then fit the model for each segment)
    -sg       Length (i.e. a number of bins) of a segment (in the case the method is set to "segmentation")
    -mso      The minimum overlap (i.e. a number of bins) between two segments (in the case the method is set to "segmentation")
    -zero     A constant to replace the zero value to take the log
    -of       The output model file
  6. Example: The script file "fitting.sh" (in folder "Examples") is to fit the model of chr22 of GM12878 from Schmitt et al. data
    a. Run the script by
      cd Examples
      ./fitting.sh
    b. The output model file is "GM12878.40kb.chr22.model" in folder "Examples/Output".
    c. In the model file, 1st, 2nd and 4th columns are alpha, beta, and the insulator respectively.
  7. For your convenience, we also provide models (in the folder "Model") that we fitted for GM12878 from Rao et al. data at 5kb resolution.
<br>
################
II. Calculate TAD-fusion score from a model
  1. Compile the source code by running the script
      ./compile_cal_tad_fusion_score.sh
  2. If the compilation is successful, an executable file "cal_tad_fusion_score" will be generated in the folder "src"
  3. Options for calculating the TAD-fusion score
    -md       Model directory, model files must be renamed as chr1.model, chr2.model, ..., chrX.model 
    -f        The file that stores deletions that we need to calculate the TAD-fusion score, the file format has three columns (e.g. one row is "chr2    221278232       223014332")
    -mnl      The minimum length (a number of base pairs), any deletion that is shorter than this threshold will be skipped
    -mxl      The maximum length, any deletion that is longer than this threshold will be skipped
    -w        The window length (a number of bins) around the deletion to calculate the TAD-fusion score
    -d        The delta value threshold to consider if a bin pair is interacted or not.
    -o        The output file, the file format has four columns where the last one is the TAD-fusion score  
  4. Example: Script files in the folder "Examples" ("1kg_script.sh", "GreatApe_script.sh", "TCGA_script.sh", "disease_script.sh", "inferred_disease_script.sh") are to calculate the TAD-fusion score of 1KG deletions, GreatApe deletions, TCGA deletions, disease deletions and inferred disease deletions (from files in the folder "Data")
    a. Run the script
      ./1kg_script.sh
      ./GreatApe_script.sh
      ./TCGA_script.sh
      ./disease_script.sh
      ./inferred_disease_script.sh
    b. The output files are in the folder "Examples/Output"
    c. In each output file, the last column is the TAD-fusion score

