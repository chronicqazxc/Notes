# Upload files to GoogleDrive

The tutoriol introduce you how to upload files to GoogleDrive from scratch setup service account to write script in Fastfile.

## GoogleDrive
1. Setup Google service account.
```
1. Open [GoogleAPI](https://console.developers.google.com/apis/dashboard)
2. Create a Project
3. Create a servcie account under [service accounts](https://console.developers.google.com/iam-admin/serviceaccounts)
3. Go to [Credentials](https://console.developers.google.com/apis/credentials)
4. Select `Create credentials -> Service account Key`
5. Download the credential json file
6. Invite service account to your TeamDrive
```

## Fastlane
1. Install [fastlane plugin google drive](https://github.com/bskim45/fastlane-plugin-google_drive)
```
fastlane add_plugin google_drive
```
2. Put the credential json in your project
3. Write code `GoogleDrive.rb`
```ruby

def create_folder_in_team_drive_test
    create_google_drive_folder(
                               drive_keyfile: "#{pwd}/drive_keyfile.json",
                               folder_id: "#{folder_id}",
                               folder_title: 'create_folder_in_team_drive_test'
                               )
end

def upload_file_to_team_drive_test
    upload_to_google_drive(
                           drive_keyfile: "#{pwd}/drive_keyfile.json",
                           service_account: true,
                           folder_id: "#{folder_id}",
                           upload_files: ["#{pwd}/testFile1", "#{pwd}/testFile2"]
                           )
end

def create_folder_in_team_drive(folder_title)
    create_google_drive_folder(
                               drive_keyfile: "#{pwd}/drive_keyfile.json",
                               folder_id: "#{folder_id}",
                               folder_title: folder_title
                               )
end

def upload_file_to(folder_id, files)
    upload_to_google_drive(
                           drive_keyfile: "#{pwd}/drive_keyfile.json",
                           service_account: true, # False if it is not a service account.
                           folder_id: "#{folder_id}",
                           upload_files: files
                           )
end

def pwd
    begin
        sh("pwd").strip
    end
end
```
4. Write a new `lane` (TestCode)
```ruby
lane :create_and_upload_file_test do
      create_folder_in_team_drive('fastlane_created')
      folder_id = Fastlane::Actions.lane_context[Fastlane::Actions::SharedValues::GDRIVE_CREATED_FOLDER_ID].to_s
      upload_file_to(folder_id, ["#{pwd}/testFile1", "#{pwd}/testFile2"])
end
```

# Conclusion
Fastlane is a very flexible tool that can accomplish any tasks into your CICD flow, I will share more example in the future.

# References
https://github.com/gimite/google-drive-ruby/blob/master/doc/authorization.md#service-account 
https://github.com/bskim45/fastlane-plugin-google_drive 
