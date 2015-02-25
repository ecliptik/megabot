# megabot.sh
megabot.sh is a command line tool for Linux systems that uses [Megatools][megatools] to upload files, get information on them from [Mega][mega], and emit messages to a [Slack][slack] channel.

[megatools]: https://github.com/megous/megatools
[mega]: https://mega.co.nz
[slack]: https://www.slack.com/
[webhooks]: https://api.slack.com/incoming-webhooks
[curl]: http://curl.haxx.se/

### Setting up megabot.sh

Megabot is fairly simple with only a few dependencies:

1. [Mega][mega] account
2. [Megatools][megatools]
3. [Curl][curl]
4. [Slack][slack] [Incoming Webhooks][webhooks]

To Install:

1. Install and configure dependencies
2. Modify megabotrc and copy to desired location (eg ${HOME}/.megabotrc)
3. Place megabot.sh somewhere in your path and chmod +x (eg ${HOME}/bin)
4. Run megabot.sh with desired options and required filename

### Running megabot.sh

You can upload a file to Mega:

    % megabot.sh -u -f tokyo.wmv

You'll see output on upload progress:

    Uploading file: tokyo.wmv to /Root/megabot
    tokyo.wmv: 92% - 10.2 MiB of 11.2 Mib
    Uploaded tokyo.wmv

You can get information on on a file in Mega:

    % megabot.sh -g -f tokyo.wmv

You'll see output of information on the file:

    File information on Mega:
    tokyo.wmv 11.2 MiB
    https://mega.co.nz/#!YRtD0DoI!iFFsJMze-DHLb343VZ1LMqvqsVF65vbG8LwzYyE98rg

You can send file information to Slack:

    % megabot.sh -s -f tokyo.wmv

You'll see output of the curl command to post to a Slack webhook:

    Slack command: eval curl -X POST --data-urlencode 'payload={"channel": "#megabot", "username": "megabot", "text": "tokyo.wmv 11.2 MiB\nhttps://mega.co.nz/#!YRtD0DoI!iFFsJMze-DHLb343VZ1LMqvqsVF65vbG8LwzYyE98rg", "icon_emoji": ":megabot:"}' https://hooks.slack.com/services/YOURKEYHERE  >/dev/null 2>&1

You can do all these things at once too:

    % megabot.sh -a -f tokyo.wmv

If you don't like output you can make any options quiet:

    % megabot.sh -q -u -f tokyo.wmv
    % megabot.sh -q -s -f tokyo.wmv
    % megabot.sh -q -a -f tokyo.wmv
