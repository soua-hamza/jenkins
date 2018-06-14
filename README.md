# jenkins
jenkins script


#!/usr/bin/env bash
source ~/.bash_profile

cd JenkinsSimplePocProject
pod install

------------------------------------

#!/usr/bin/env bash
source ~/.bash_profile

cd JenkinsSimplePocProject
agvtool new-version -all ${BUILD_NUMBER}

------------------------------------



#!/usr/bin/env bash
source ~/.bash_profile

echo "will start archiving Release"

rm -r "${WORKSPACE}/build/"

/usr/bin/xcodebuild -verbose -scheme JenkinsSimplePocProject -workspace "${WORKSPACE}/JenkinsSimplePocProject/JenkinsSimplePocProject.xcworkspace" -configuration Release clean archive -archivePath "${WORKSPACE}/build/JenkinsSimplePocProject.xcarchive" "BUILD_DIR=${WORKSPACE}/build" DEVELOPMENT_TEAM=99J6CKC79H


------------------------------------

#!/usr/bin/env bash
source ~/.bash_profile

echo "will start export archive"
echo "${WORKSPACE}"
/usr/bin/xcodebuild -verbose -exportArchive -archivePath "${WORKSPACE}/build/JenkinsSimplePocProject.xcarchive" \ -allowProvisioningUpdates -exportPath "${WORKSPACE}/IPA/JenkinsSimplePocProject_Build_${BUILD_NUMBER}" -exportOptionsPlist "${WORKSPACE}/JenkinsSimplePocProject/exportOptions-adhoc.plist"

------------------------------------





#!/usr/bin/env bash
source ~/.bash_profile

curl https://upload.diawi.com/ -F token='jhInx69gA2fOGV00y0PpD0ym7A6QgUx60uv1AOLIjc' \
-F file=@${WORKSPACE}/IPA/JenkinsSimplePocProject_Build_${BUILD_NUMBER}/JenkinsSimplePocProject.ipa \
-F comment='uploaded by jenkins' \
-F callback_emails='email@email.fr','email@email.fr.fr'

------------------------------------




#!/usr/bin/env bash
source ~/.bash_profile

#gdrive installation and configuration from https://github.com/prasmussen/gdrive
#lanch gdrive about to get access to the drive more detail here https://www.howtoforge.com/tutorial/how-to-access-google-drive-from-linux-gdrive/

#echo "upload ipa to google drive"

#/usr/local/Cellar/gdrive/2.1.0/bin/gdrive upload --recursive --parent 1cBFucqs6Cvz9OZJCmVbE-k2Ee-4ERUcC ${WORKSPACE}/IPA/JenkinsSimplePocProject_Build_${BUILD_NUMBER}

#tab=$(/usr/local/Cellar/gdrive/2.1.0/bin/gdrive list --query "'1cBFucqs6Cvz9OZJCmVbE-k2Ee-4ERUcC' in parents and  name = 'JenkinsSimplePocProject_Build_${BUILD_NUMBER}' and trashed = false")
#set -- $tab
#echo "build folder Id: $6"
#echo "share google drive folder"

#get new access token https://help.talend.com/reader/Ovc10QFckCdvYbzxTECexA/EoAKa_oFqZFXH0aE0wNbHQ
#/usr/local/Cellar/gdrive/2.1.0/bin/gdrive share $6 --type user --email email@email.fr
#/usr/local/Cellar/gdrive/2.1.0/bin/gdrive share $6 --type user --email email@email.fr
#/usr/local/Cellar/gdrive/2.1.0/bin/gdrive share $6 --type user --email email@email.fr


