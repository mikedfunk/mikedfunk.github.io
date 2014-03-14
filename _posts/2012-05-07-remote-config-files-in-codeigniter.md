---
title: Remote Config Files In CodeIgniter
layout: post
---

I ran into a situation recently where I had multiple CodeIgniter apps which depended on the same config values. No problem, right? Just use a common third_party folder. That would work, except they were on different servers! My solution was to echo the config as JSON in one place, grab the JSON in other apps and load them as config values. Now you can do the same!

<!--more-->

## Setup

1. Install sparks at [GetSparks.org](http://getsparks.org)
2. Install the [curl_load](http://getsparks.org/packages/curl_load/show) spark

## Usage

First, do this in your config file:

{% highlight php %}
    <?php // DON'T put the usual !defined(BASEPATH) part up here
     
    $config['this_key'] = 'value';
    $config['that_key'] = 'value';
     
    // if it's not loaded by CodeIgniter, echo it as JSON so
    // we can grab the keys/values remotely
    if (!defined(BASEPATH)) echo json_encode($config);
{% endhighlight %}

Now in your controller, use the curl_load spark to load the config file:

{% highlight php %}
    <?php if ( ! defined('BASEPATH')) exit('No direct script access allowed');
     
    class test_controller extends CI_Controller
    {
        public function index()
        {
            // replace x.x.x with version number
            $this->load->spark('curl_load/x.x.x');
     
            $config_url = 'http://example.com/path/to/config.php';
            $this->curl_load->load_config($config_url);
        }
    }
{% endhighlight %}

If you need to secure the values of the config file, you can add optional http authentication credentials:

{% highlight php %}
    $this->curl_load->load_config(
        'http://example.com/path/to/config.php', 
        'http_auth_username', 
        'http_auth_password'
    );
{% endhighlight %}

Or you could load an array of config files:

{% highlight php %}
    $this->curl_load->load_config(
        array(
            array(
                'url' => 'http://url1.com/config.php'
            ),
            array(
                'url' => 'http://url2.com/config.php',
                'username' => 'optional_http_auth_username',
                'password' => 'optional_http_auth_password'
            )
        )
    );
{% endhighlight %}

Last but not least: You can set it to autoload config files in ```config/curl_load.php```. Just add your config files in the same array format as above:

{% highlight php %}
    $config['curl_autoload'] = array(
        array(
            'url' => 'http://url1.com/config.php'
        ),
        array(
            'url' => 'http://url2.com/config.php',
            'username' => 'optional_http_auth_username',
            'password' => 'optional_http_auth_password'
        )
    );
{% endhighlight %}

This is really cool, especially when you autoload the spark as well. Then your config values will automatically be loaded without you having to do anything!

{% highlight php %}
    $autoload['sparks'] = array('curl_load/x.x.x');
{% endhighlight %}

If this helps you, leave me a comment. Have fun!
