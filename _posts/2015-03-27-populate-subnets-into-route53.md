---
layout: post
title:  "Populate subnets into Route53"
redirect_from:
  - /cloud/populate-route53-subnet.html
date:   2015-03-27 06:50:17
category: cloud
tags: [devops, dns, aws, route53, ruby]
---

Recently I was working standarizing network addressing and host names as part of a deployment inside an [AWS][AWS] [VPC][VPC], so I came up with this solution. This script will associate IP addresses ranging from `192.168.10.2` to `192.168.10.254` and from `192.168.11.2` to `192.168.11.254` with DNS A records named ip-192-168-10-X.lan.example.net and ip-192-168-11-X.lan.example.net. This can also be very useful when dealing with services rescricted by URLs and you need your developers to be able to publish them using their workstations.

{% highlight ruby %}
# Force v1.x of the AWS SDK
gem 'aws-sdk', '< 2.0.0'

require 'rubygems'
require 'aws-sdk'
require 'colorize'

acces_key_id = 'YOUR_KEY_ID'
secret_access_key = 'YOUR_SECRET_KEY'
zone    = 'lan.example.net'
zone_id = 'RUTE53_ZONE_ID'

ttl = 86400 # 24 hours

r53 = AWS::Route53.new( :access_key_id => acces_key_id, 
                        :secret_access_key => secret_access_key )
records = r53.hosted_zones[zone_id].rrsets

nets = %w( 192-168-10 192-168-11)

nets.each do |net|
  net_ip = net.gsub('-', '.')
  puts ">>>> #{net_ip}.0/24 <<<<".colorize(:red)
  (2..254).each do |i|
    records.create("ip-#{net}-#{i}.#{zone}.", 'A', :ttl => ttl, 
                    :resource_records => [{:value => "#{net_ip}.#{i}"}])
    puts "ip-#{net}-#{i}.#{zone} => #{net_ip}.#{i}"
  end
end
{% endhighlight %}

This script definetely saved me a lot of clicks. Enjoy yourself!

[VPC]: http://aws.amazon.com/vpc
[AWS]: http://aws.amazon.com
