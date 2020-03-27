---
layout: post
title:  "Quarantine_and_progress"
image: ''
date:   2020-03-27 10:08:00
tags:
- Quarantine
description: 'Quarantine_and_progress'
categories:
- blog, AWS_Migration, Devops
---

## Quarantine and progress

<p>
A lot has happened over the past few months. Working on our AWS Infrastructure has certainly been a challenge, but something I've been enjoying greatly.
<br>
<br>
I certainly didn't expect this corona pandemic to take place, but I'm fortuntate to work in a job field where working from home is relatively easy. A shame that this isn't the same for everybody unfortunately; so I really do feel for those that are experiencing issues because of this epidemic.
</p>
<p>
In regards to AWS, migrating this huge monolithic application into separate services on AWS has certainly been interesting. A ton of work has been put into place. It's definitely been a challenge, but can now see the light at the end of the tunnel!! I've enjoyed pretty much every single step of this, and the learning experiences that I've had, including knowledge gained. Always more to learn!
<br>

I think the main issue in regards to it; has been that for each thing that you do, there's always an extra 2 or 3 things that then need to be put into place for it to then work. Talk about project scope creep. Problem is, it doesn't explicitly tell you what those extra things are, so having to solve those problems has definitely been both infurating and enjoyable at the same time.
<br>
<br>
</p>
<p>

### Notable things that have been done

- Terraform to describe all of our infrastructure. The most painful part was trying to get transcoding working correctly.
    - A somewhat annoying issue, was trying to get the client_vpn working. Terraform doesn't quite have full support for it yet, so it required hacking the remote state file to get it implemented. Below is a snippet that was implemented into the state file to actually get that working.
```
resources : [
........
{
      "mode" :"managed",
      "type" :"aws_ec2_client_vpn_network_association",
      "name" :"vpn-prod",
      "provider": "provider.aws",
      "instances":[
        {
          "schema_version": 0,
          "attributes" :{
            "client_vpn_endpoint_id" : "cvpn-endpoint-ccccccc",
            "id": "cvpn-assoc-xxxxxx",
            "security_groups": ["sg-dddddddd"],
            "status" :"associated",
            "subnet_id":"subnet-bbbbbbb",
            "vpc_id": "vpc-aaaaaaaa"
          }
        }
      ]
    }
]
```

- Codebuild - We've been using codebuild to create all of our application servers, via packer. So I've been pretty busy scripting the entirety of our servers into our Application_packer repo.
    - Definitely been fun, interesting and challenging. Notably, how to get our secrets from AWS_SSM and into a dotenv file. It's a simple(ish) bash loop, which seems to work really well. You can see it below.

```
#!/usr/bin/env bash
set -x
#
# A .env file builder for use when
# creating  server images
#
# Populate with this:
# aws ssm put-parameter --region eu-west-2 --name env --tier Advanced --type SecureString --value "$(cat env)" --overwrite
#
#SERVER_TYPE pulled from app.json

#Location of repository where code_base is installed.
#$SERVER_TYPE is pulled from the app.json for packer.
REPO_LOCATION="/var/www/$SERVER_TYPE"

# The environment we are building for
# Most like this comes from an existing variable
#Change this in future
ENVIRONMENT="production"

# This is the full path to the template file.
# You may need to generate the second part of
# this based on another variable
#Need to add another variable based on the packer var of Application, Application-worker etc
#Server type defined in packer json
TEMPLATE="${HOME}/env/${ENVIRONMENT}-$SERVER_TYPE.env"

# The full path to the target file
#Repo_location defined in packer json.
OUTPUT="$REPO_LOCATION/.env"

# The pattern to look for in the template file
# Don't edit this unless we change the rules
PATTERN="<([a-z0-9\-\_]+)>"

# Ensure our OUTPUT file is present in an empty form
if test -f "$OUTPUT"; then
    rm "$OUTPUT"
fi
touch "$OUTPUT"

# Read the template file line-by-line
while IFS= read -r LINE
do
    # Perform a pattern check on the current line
    [[ $LINE =~ $PATTERN ]]
    # If we have a match, perform the swap
    if [[ ${BASH_REMATCH[0]} ]]
    then
        # Swap out our environment setting
        if [ "${BASH_REMATCH[1]}" == "current_environment" ]; then
            LINE=${LINE/${BASH_REMATCH[0]}/${ENVIRONMENT}}
        # Swap out a parameter store value
        else
            PARAMETERNAME="${ENVIRONMENT}_${BASH_REMATCH[1]}";
            RESPONSE="$(aws ssm get-parameter --name "${PARAMETERNAME}" --with-decryption --region eu-west-2)"
            LASTERROR=$?
            if [ ${LASTERROR} == '0' ]
                then
                    PARAMETERVALUE=$(jq -r ".Parameter.Value" <<< "$RESPONSE")
                    LINE=${LINE/${BASH_REMATCH[0]}/$PARAMETERVALUE}
                else
                    continue
                fi
        fi
    fi
    # Append the current line to our OUTPUT file
    echo "$LINE" >> "$OUTPUT"
done < "$TEMPLATE"
```
I have more to write about which I'll come back to when I get time, but for now, this is the next update. I'll see about updating more reguarly, with difficulties or challenges I've found and overcome whilst working on this project.

Ollie over and out.
