---
layout: post
title: Wifi signal strength in oh-my-zsh 
type: post
status: publish
published: true
---
I recently switched theme in [oh-my-zsh](http://ohmyz.sh/) to [powerlevel9k](https://github.com/bhilburn/powerlevel9k) while the docs cover most things the wifi signal [example](https://github.com/bhilburn/powerlevel9k#custom_command) was Linux only so I modified it to work on MacOS (only tested on Sierra) and modified to use [nerd-fonts](https://github.com/ryanoasis/nerd-fonts)  as its not the same unicode as in the docs example.

{% highlight shell %}
zsh_wifi_signal(){
    local signal=$(/System/Library/PrivateFrameworks/Apple80211.framework/Versions/Current/Resources/airport -I | grep CtlRSSI | awk '{print $2}')
    local color='%F{yellow}'
    [[ $signal -gt -60 ]] && color='%F{green}'
    [[ $signal -lt -70 ]] && color='%F{red}'
    echo -n "%{$color%}\uf424 {% raw  %}%{%f%}{% endraw %}"
}

POWERLEVEL9K_CUSTOM_WIFI_SIGNAL="zsh_wifi_signal"
POWERLEVEL9K_CUSTOM_WIFI_SIGNAL_BACKGROUND="black"

POWERLEVEL9K_RIGHT_PROMPT_ELEMENTS=(status custom_wifi_signal load disk_usage battery)

POWERLEVEL9K_MODE='nerdfont-complete'
{% endhighlight %}

So with that in my `.zshrc` my prompt looks like this right now
![everything]({{ site.url }}/assets/powerlevel9k.png)
