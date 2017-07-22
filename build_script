#!/bin/bash
# 
# Added by Parksungho
#

clear

# set envsetup for android
source ./build/envsetup.sh

echo 
echo =============================================
echo              Custom Build System
echo =============================================
echo 

# definition
model_prefix=
build_mode=
build_project_name=
project_filename=model_list.txt
options=

function deleteProjects {
    for (( i=0; i<=${#options[@]}; i++ ))
    do
        options=("${options:i}")
    done
}

function loadProjectData {
    if [ ${#options[@]} -gt 1 ] ; then
        deleteProjects
    fi

    for line in `cat $project_filename`
    do
        options=(${options[@]} ${line})
    done

}

function initProjectsList {
	project_num=${#anc_projects[@]}

	for (( i=0; i<=$project_num; i++ ))
	do
	options=(${options[@]} ${anc_projects[i]})
	done

}

function setBuildMode {
	echo "[1] user, [2] userdebug"
	read -n1 -p "Choose :" selData
	echo 

	case $selData in
		"1") build_mode=user
		;;
		"2") build_mode=userdebug
		;;
	esac

	startBuild
}

function startBuild {
	build_project_name=$model_prefix-$build_mode

	echo "The Project is "$build_project_name
	echo
	echo "Please, Waiting..."
	echo 

	if [ -n $model_prefix ] ; then
        lunch $build_project_name
        make -j16
	else
		echo failed
	fi
}

# Load projects from the model list file.
loadProjectData

# Start Build Script
echo Choose the project....

select opt in "${options[@]}"
do
	model_prefix=$opt
        echo "Selected : "$model_prefix
	echo 
        setBuildMode
	break
done
