# DeepCC
This is a tool that extracts the intracranial and corpus callosum area as a biomarker, normalized corpus callosum, for neurodegeneration in multiple sclerosis.

#Instructions:

#Pre-processing

The first step is to extract the middle slice from your T2-weighted MRI sequence. For this you will apply the script "Preprocessing.py". This script will extract the middle slice, pre-process and reshape the target slice and make it compatible with the DeepCC model. You have to make sure to fill in your source path (where your MRIs are located) as well as the destination path (where you want the output). Below is an example of the paths:

    img_path = '/Users/yourcomputer/MRI/where_you_have_your_MRI'
    dest_path = '/Users/yourcomputer/output'

After this, we highly recommend you control your data as to make sure that the middle slice actually represents something close to the anatomical middle. Structures that speak for an anatomical middle are: the cerebral aqueduct, fornix, superior/inferior colliculus, a well-defined corpus callosum.


#The Model

You are now ready to apply the model on your data. In the file "Main" you will enter the path to where your pre-processed images are. You will also add the path to the two models (corpus callosum and brain). The predictor will combine these two models and output the segmentation along with the normalized corpus callosum value.



Below is the Predictor. As mentioned above, fill out the path to the images being segmented. Download the two models here: https://ki.box.com/s/r3og7cjrpxqtfd2u185jo9od5wn5rh4i
https://ki.box.com/s/o3eanuvv86d1hkyn1axchejbwbhjqd1m


Important: place the corpus callosum model before the brain. This will then export an output that is corpus callosum divided by the intracranial area. If you place them in reverse order you will end up with the intracranial area normalized to the corpus callosum.


    prd = Predictor(dl_c, image_path='/path_to_images_to_be_segmented/*.jpeg')
    prd.load_and_predict_both_models(model_paths=['/path_to_the_saved_model_corpus_callosum/model/',
                                '/path_to_the_saved_model_brain/model/'])
