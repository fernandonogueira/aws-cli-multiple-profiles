# AWS CLI Multiple Profiles

This is a simple project to make it easy to switch profiles when using the AWS CLI tool.

New terminal tabs/windows/sessions will use the previously used profile by default.

### Installing

#### Step 1

Add your profiles to `~/.aws/credentials` file like below

```ini
[default]
aws_access_key_id = ACCESS_KEY_DEFAULT
aws_secret_access_key = SECRET_KEY_DEFAULT

[some-prof1]
aws_access_key_id = some-prof1-access-key
aws_secret_access_key = some-prof1-secret-key
```

#### Step 2

Update your `.bashrc` or `.zshrc` file (located at `~/.bashrc` or `~/.zshrc`)

```bash
if [[ -f ~/.aws/selected_profile ]]
then
  selectedAwsProfile=$(cat ~/.aws/selected_profile)
  echo "Selected AWS Profile: $selectedAwsProfile"
  export AWS_PROFILE=$selectedAwsProfile
else
  echo "Selected AWS Profile: default"
  export AWS_PROFILE=default
fi

function awsProfile() {
  if [ "$1" == "" ]
  then
    awsProfile = "default"
  else
    awsProfile=$1
    echo $awsProfile > ~/.aws/selected_profile
    echo "Selected AWS Profile: $awsProfile"
  fi
  export AWS_PROFILE=$awsProfile
}

```

Done!

### Usage

To change profile run:

`awsProfile YOUR_PROFILE`

```
➜  ~ awsProfile myProfile
Selected AWS Profile: myProfile
```

When you create new terminal sessions, your last used profile will be automatically selected

```
Last login: Mon May  7 11:53:53 on ttys007
Selected AWS Profile: myProfile
➜  ~
```