# EPiC 2023: The Emotion Physiology and Experience Collaboration (additional details)

## 1. The goal of the EPiC 2023 competition
We aim to (1) establish the best approaches to moment-to-moment inference of valence and arousal from physiology, (2) compare how model accuracy scores vary across different validation scenarios, and (3) promote open science.

## 2. The task
The task is to predict continuous values of valence and arousal based on the available physiological data. Formally, this is a regression problem.

## 3. Experiment description
Some details on the experiment will be concealed in order to avoid bias. All information will be disclosed at the end of the competition.

The data will be from an experiment on emotion annotation conducted in a laboratory setting. Study participants watched emotional stimuli and annotated their emotions continuously in arousal-valence space. During the experiment, the following physiological signals were recorded:
- blood volume pulse (bvp)
- electrocardiogram - 1 electrode (ecg)
- electromyograms from three muscles:
	- corrugator supercilii (emg_coru)
	- trapezius (emg_trap)
	- zygomaticus major (emg_zygo)
- electrodermal activity / galvanic skin response (gsr)
- respiration rate (rsp)
- skin temperature (skt)

All physiological signals were recorded with the sampling frequency of 1kHz, and annotations were recorded with the frequency of 20Hz.

## 4. Data structure
Data will be divided into four scenarios, each representing a different validation approach:

1. Across-time scenario corresponds to the hold-out validation approach that respects chronology. Each sample is divided into training and test parts based on the time. A sample represents a single person watching a single video - first part of the activity is in the train set and the later part in the test set.

This scenario analyzes how well a model utilizes knowledge obtained from the past data to the new data from the same set of participants and stimuli.

2. Across-subject scenario matches the leave-N-subjects-out validation approach. Participants are divided into random groups. All the samples of a given group of participants belong either to the train or test set, depending on the fold. There are 5 folds in this scenario and each fold leaves out a different set of subjects.

This scenario validates a model’s ability to generalize knowledge obtained from a group of people to other, previously unseen, people.

3. Across-elicitor scenario follows the leave-one-stimuli-out validation approach. There are two samples (videos) per each quadrant in arousal-valence space, and both are excluded in a given fold. There are 4 folds in total, each excluding one arousal-valence quadrant.

This scenario validates how well models trained on three arousal-valence quadrants can infer states experienced in the fourth quadrant.

4. Across-version scenario resembles the hold-out validation approach that doesn’t necessarily respect chronology. There are two samples per arousal-valence quadrant, so one will be used to train the model while the other to test it. Thus, this scenario has 2 folds.

This scenario validates how well models trained on one version of the quadrants can infer states experienced in the other version of the quadrants.

Similarly to the first scenario, this scenario analyzes how well a model performs for the same set of participants and a similar task.

For each scenario, there will be both training and test data sets. Teams can further divide the training set (e.g., into training and validation) if the woudl like.

In the test set, the length of the physiology is 20 seconds longer than the length of the self-annotations (ground truth). This is to allow building models that utilizes time windows of up to 20 seconds long – 10 seconds of physiology before and 10 seconds after the annotation timestamp. Please note, teams can decide what architecture, which physiological signals, which features, what window size, to use.

Data files in test sets (not yet posted) will have columns and timestamps defined, but no data. The task is to predict arousal and valence levels for all timestamps.

## 6. Requirements and submission procedure
- No cheating
- Code should be clean, well commented, and reproducible, and it will [eventually] be uploaded to a public project repository
- Willing to serve as a co-author on a paper describing the challenge results

## 7. Additional information and materials
Using Python is not required but we strongly encourage it.