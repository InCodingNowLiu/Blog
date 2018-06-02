title: 'IOS 判断是否连接vpn '
author: incodingnowliu
date: 2018-06-02 20:18:15
tags:
---

# iOS 判断是否连接vpn 
```bash

- (BOOL)isVPNConnected{
    struct ifaddrs *interfaces = NULL;
    struct ifaddrs *temp_addr = NULL;
    int success = 0;
    
    // retrieve the current interfaces - returns 0 on success
    success = getifaddrs(&interfaces);
    if (success == 0) {
        // Loop through linked list of interfaces
        temp_addr = interfaces;
        
        NSString *str = @"";
        while (temp_addr != NULL) {
            NSString *string = [NSString stringWithFormat:@"%s" , temp_addr->ifa_name];
            str = [NSString stringWithFormat:@"%@,%@",str,string];
            NSOperatingSystemVersion version =[NSProcessInfo processInfo].operatingSystemVersion;
            NSString *versionStr = [NSString stringWithFormat:@"%ld",version.majorVersion];
            NSInteger versionValue = [versionStr integerValue];
            if (versionValue >= 10.0)
            {
                if ([string rangeOfString:@"ipsec"].location != NSNotFound ){
                    return YES;
                }
            }
            else
            {
                if ([string rangeOfString:@"tap"].location != NSNotFound ||
                    [string rangeOfString:@"tun"].location != NSNotFound ||
                    [string rangeOfString:@"ppp"].location != NSNotFound){
                    return YES;
                }
                
            }
            
            temp_addr = temp_addr->ifa_next;
        }
    }
    
    // Free memory
    freeifaddrs(interfaces);
    return NO;
}

```