![](https://lh3.googleusercontent.com/yfauRkorcR5tsFglEdZxcCNB9Q8gvT4mggnkshWrB8q_-cYqvLyIQ3E6ice1-LyU_1RPOSOBQGJV4ioYEMUHmnaA-vR0-QEf6n2DMsuSKShlMMkT3icnW8YPWsmNZqpHNCoQOXPJagUvsjXvUA)

![](https://lh4.googleusercontent.com/WklkdY_mjQ-WBwYKvAXSKjASdEiaovVgOuy133k8FckQasbq6zfUE8IOanAYXWWTk55OFwO2_02oyD7aUGUl27s-3ukZ6bnurY3tdMs7qIehSPukBaWLyZMblNzI6cfsN1fU8klkGLSyCq8n7g)

# Zero Trust AWS CN-Series

## QwikLab Guide

# Overview

A Zero Trust implementation should provide security administrators with the visibility and the ability to secure traffic between the various applications. 

## Hands-On Lab – Palo Alto Networks Product Coverage

- **[CN-Series Virtual Next-Generation Firewalls](https://www.paloaltonetworks.com/network-security/cn-series)**
    - Protect Kubernetes Containers
    - Keep cloud native applications nimble and secure with the industry's first ML-Powered Next-Generation Firewall (NGFW) built for Kubernetes® environments.

- **[Panorama™](https://www.paloaltonetworks.com/network-security/panorama)**
  - Consolidate policy management. Panorama™ network security management simplifies policies across infrastructures and clouds. Seamless integration. Increased oversight.
  - Panorama can be deployed as a virtual appliance on VMware ESXi™ and vCloud<sup>®</sup> Air, Linux KVM, and Microsoft Hyper-V<sup>®</sup>.

# Application Environment Overview

## Launch the lab environment

In this section, we will launch the lab environment. These are the steps that we will accomplish at this time.

- Start the lab on your designated Qwiklab account.
- Login to the AWS Console using the provided credentials and set up  IAM roles
- Subscribe to the Panorama appliance on the AWS Marketplace.
- Deploy lab environment using Terraform
- Deploy the CN-Series firewalls
- Deploy a sample application for the activity 


## Start Qwiklabs lab environment and login to AWS

1. Once you login to [paloaltonetworks.qwiklabs.com](https://paloaltonetworks.qwiklabs.com/), the Home page should display the Labs that you have access to. Identify and click on the Lab that says "_Zero Trust AWS CN-Series Lab_".

![](https://lh5.googleusercontent.com/bu42_RDRb5vlFF6ZNIx2OtYZol7gWgScvxzAuwUTNOqWLLtlwuD077ozyfS2t9Er377XzYpPTxraYPBmMryLMW6TbR2NpMNygzIfTEpT1B2pwQSFkPTSKD-ng-pi8vfMLtMWseOQpHS36z2VyA)

2. On the page that opens up, click on _CN-Series Zero Trust lab_.

![](https://lh3.googleusercontent.com/UgERm-Dmo0oAuPgIq7zcZbg3CuUn1pRkER6bbHexmEXN-1MB9Z5MmhdwAxwMAS874-B6UIcxB28KmnQ_T7MLfI4rn3aqJP2pCjLf0lytF_hTcZMCat2vb2fkQMtAa5MD4c8NvjtD5cb-hsOXxA)

3. On the Qwiklab environment, Click on _Start Lab_ Button to start the lab.

![](https://lh5.googleusercontent.com/uZswWQ3eJyJ78dDiDDWMuqqfyDqYPOT50WppC4KgVnWEKT2DP8oyYuOHTTIm4CGSh12odVxYtJ3UuXe2Ft_aH2DOjXRAFDPGgPR9iQm6ikrBT4iTZnwqNDBf3TfsR6GDU28xBE7ZTMF44NRAIg)

At this point, Qwiklabs will build an AWS account for you. In order to access the EC2 application instances via SSH in your environment, you will be using keys generated by Qwiklabs. There are two types of keys generated; PEM and PPK keys.

4. If you are on a MAC, you will be using ‘Terminal’ to connect to the devices via SSH. For this, click on the “Download PEM” link. This will download a file named “qwikLABS-L\*\*\*\*\*-\*\*\*\*\*.pem”.

   - Make sure to note the location where the file is downloaded. On a Mac, by default, it will be downloaded to “/Users/&lt;username>/Downloads”

5. If you are using a windows laptop to access this lab, you will need to have a ssh application like PuTTY installed. ![](https://lh4.googleusercontent.com/KztKlSkNNaQU61dPFGIAxrgDK8OSeSy6SGbcfPaO4Yji-EzBR_leZ02KN3u9_Twcj1qVL5B0OYOD_hZt2z1YWT5NQI53PzHl4HOzJAGxMz5EdedRkG3z62p7aouOzV-bAyWY3cDPJBwdkLrrpw)

   - In this case, click on the “Download PPK” link. This will download a file named “qwikLABS-L\*\*\*\*\*-\*\*\*\*\*.ppk”.

![](https://lh4.googleusercontent.com/9mJrciMHAaP929OpmukkN2K7nJZAEWqHY9tiAOaAdJZPeMc7My1tTRJKj3ZNhbfKWbTcvY8gBjfkQ0Bhxlbxy3eptSvk_CeFIrdugaI8MYkyz_g_d6McJocu7mtDxymFRbvpoEgS9fqwya0Ipw)

6. To login to the AWS environment, right click on “Open Console’ and “Open link in Incognito window” for Chrome-based browsers. For other browsers, use the appropriate option to open the AWS Console in a new private tab.

![](https://lh6.googleusercontent.com/uT9aD3yPqEH281H3ArxEeD__pjYDaJMSyv6CN0Fe78cnAjkNa_TA5LMKqHw3hUNUkWGI-bO3YuxXSuehWHvbIPR-EL616pesbcCxdLDkoeYrApT3AuvRXXPazBH1TIIl4IUGUXGL0mO4faL2aSc)

7. On the AWS Console, copy over the IAM username and password from the previous tab.

![](https://lh5.googleusercontent.com/b9Wwy3UiNDKna9cJkaV0SvyP9YFhIJV9Q0t_mqzvjRlo_RUNXNlqxxhZ1gDOen_RTkMxQQSoLRG3QIXT7GqvnzbkgpxrqBASd8Be1ZSVas_o5DNtwfmcjnfhwwfysDITt2KHxhC6W33pZEiykg)![](https://lh4.googleusercontent.com/fpGosvriB6Z2pqvMM70L7xUCHEpmfj55-1_BaPR_pDIBxprGXVi_v_YZr1aY4kc1IFUIz7rRoELUhNFDUT51EHGSVw326zeDCBnhvd6DbpMlrvEgyIqWUMpCLY_SIbBtro2au3GYk8CetXrTlw)

8. Now, click on “Sign In”.

![](https://lh5.googleusercontent.com/J5se3uljpa6L3MK-TVqMxBBplVKQQnZ6Wrh5atg3h_RiYAZtJZgaqSAe4-uV5RCk7h3bQ-QrUSQMvOAKBDKjS6kQ4iILWerNNnnfkDN4ryx5WB1DxlyrpQyLCLhJfg_CjH98fwkre31l2hurVQ)

Once you are successfully logged in, you will land on the AWS Management Console.

![](https://lh6.googleusercontent.com/vLh-4_cDPwBtDGcH5Vq08ai8wCwVzRY_zNsCn8fxhKL493RamNO5PrZWNbxC8d54OXx1_FbVCb6z1uesMBE9kI7DW33NR31JHxIqAxCqR-_19vNYtX_uNtxasgVhDNIlfJPpVEozEwyzZcQSag)
**Figure:** The AWS Management Console

## Set up AWS Account permissions

As mentioned earlier, the Qwiklab user account, by default, does not have the permissions to AWS Marketplace and CloudShell services, which are required for the purpose of this lab. We will now edit the permissions for the Qwiklab user account to provide access to those services.

On the AWS console,

9. If you see a message for ‘new AWS Console’ click on ‘Switch now’
10. On the search bar type ‘iam’.
11. Click on the link to _IAM_. A new IAM dashboard window will open.

![](https://lh6.googleusercontent.com/prkjUS9HYswz-jjKU1lmwO6vUu5NzB-ffyeWv0hpQcnmmWFpXWtPo0pSCn90Jig1xfa6paud-ITotC500osJpEiVR1FtRmhMa5RznNJOL1pd2rceW_eBCts2zRGBWmyzOANZJrPuSIMyKmr1MQ)

12. Click on ‘2’ below users.

![](https://lh3.googleusercontent.com/6i-i100jVqCcVvg9eA6QBzy6CBTU2Q0qGoc_4vjt7X7r7AlojhYW4h84aiTeWTym5UU6hLQBtKE0o9CPudc5RW6edyylGxMl4WNbupQQwVSZMXjRy83BxBUrZsVdS7FglsS6reBkdpL6Wqimcw)

13. Click on ‘awsstudent’.

![](https://lh3.googleusercontent.com/rCDrl8lHLPx-XWCqcAe5o1IA_-N1fVLHwod7pSxLc_wzPbWh2LP_m-Ipzi9Vc4RST-3NbqqBbIr6Q2_ggKLUsEPlTBt3jACeCiDvlNkj_xtakraRHo60hDInJpFoIz4Tv2qehfnnADUsThc3_g)

14. Expand the default policy by clicking on the small triangle icon against default_policy in the list.

![](https://lh5.googleusercontent.com/DoxiUC4CM9Mt8HH2oIBS1v6jf2mUnsQmIaiZoYbY6k8A0HjLVDm5rjVXWLOpZZ_c73jGpOVqq1jXINOT1ai8nR7H8ubd5EWkSTeaYRSmt1o9pOd7DxiQjCkM_JaF8B0g9JT2Rtz2SeavwIhJNA)

15. Click on the ‘Edit Policy’ button.

![](https://lh4.googleusercontent.com/VtZe2xx-WurO_LpxfiRcRPkPgZZrWv2x0TU-2MhhDEa1OmtoucFVhC9KoIRL-jLF7Re9SouK3LbRfkzJgyeJ9Y8FA93fuF30j13iR2cSvpDFJTxjc9q0aYkLFUFcpRO-rg5zJa7NMtwBp3OP_w)

16. Click the ‘JSON’ tab.

![](https://lh3.googleusercontent.com/o44YVIRRJZkh4Q27BgCtAclylZRMrlXKvRlVoZ6JmQoSaWvTV_L6gMMUEB038lVRobt-M5xiir8OVr6jW3tCH-KW85hb0LEdnOMNv-XQbR-VniOhV8_Mh91ZBfCfI5f8Sff0ys0uP1YyCDL0ww)

17. Scroll down to the Deny policy and remove two lines (**line number 27** and **line number 36**) listed below

```
"aws-marketplace:\*ubscribe",
...
"cloudshell:\*",
```

Make sure to delete the whole line.

![](https://lh6.googleusercontent.com/gYkT0FH78QpnP24zVZPpKgSdtDLf1qaqmMb0AIpHtJ_O1B1AtirKcG28AQ_GXedKM_eFjgN7-o_2ZEeRD7syK2fdYPN_X3OVvECY9y6FbLp75EsN3lVTGBM7ptpPZCLwvoYRupOOyoaTM9wNcg)

18. Click on ‘Review policy’ at the bottom of the screen.
19. On the next screen, click on ‘Save changes’.

![](https://lh6.googleusercontent.com/iZlrM6e0CPx6Wv6ylxAU9R1wUnpAjlEj697Nu6VOd-sCOqUwhERAOB_JMCDXiRHJn_4XIQvtV-OV07Q1G98dUnS45DcxJfmwdEM5c6vF4Illor73BBw9p7_6SEqFRQ_OFH5Ky9nbeBWKk-vobQ)

20. Account setup is now complete.


## Subscribe to Panorama on the AWS Marketplace

In this section, we will deploy the AWS Cloud resources required for the purpose of this lab using Terraform. 

21. Click on ‘AWS’ on the top left hand corner to navigate to the primary console.
22. Make sure that the region is N.Virginia.

![](https://lh5.googleusercontent.com/wvbD9GAzrkzYYlrz2yh68A-bQTgY7hRvtJ9Mjk5UCk4MTJfu4jn7MEjVJ_fpFVOtk8VQsZNEY9-1Ke0xcU-wOOiZeEI7uYq9_HpB9jSMKxFOc_kcD-yMfqMZ_FCjhFhj3NCWJILT-eLJYClWlw)

23. Subscribe to Panorama.
    - Click on the link below and the page that opens up, Click on “Continue to Subscribe” and then Click on “Accept Terms”.

<https://aws.amazon.com/marketplace/pp?sku=eclz7j04vu9lf8ont8ta3n17o>

![](https://lh3.googleusercontent.com/NakhvcKUlhnLlCvSGQyuyP9yFv5NNkBK9i5zuAeB2xHhrDMezl6PolPqFmrmcQTFRXkvsFc7CsqDfE5TrnFug4U9YUVLaMgVYDZLIaQ389W8eBVsEqaNM5gX1KTjUr4boUZyB1ME9yzoRiR3DQ)
![](https://lh6.googleusercontent.com/pDi8o8qtSGly7Y3UV7cX2kIHiHmzxyFg_hzmAxRmLPn5BCow1UMSmE1fVr7K8wOU-rgspAnVxn4t2NdhcUm7xhbmVBTXNmsQzzwPltpzT0QBvAwfX5UzAOOS6xM_P41PdZSQejXdFxHgY_mJLQ)

24. Wait till Effective date changes from ‘Pending’ to today’s date. This will take a few minutes.

![](https://lh3.googleusercontent.com/L1M7PgFTujgp-C5XtxfQWH0MJbWHZI6nfzR8JDWz8H4chMkuzxyh422ZdpIQFw8ODE8eJXz8J_lYK4mK_-0l62MBaxR_hoDDXr4tFvQ0E7bp6frc76c19EyrjLYFeuZDyNSxKYmnL15IK1fzhg)


## Deploy the Lab resources using Terraform

25. From the AWS management Console, launch CloudShell using the icon on the top right side of the console.

![](https://lh6.googleusercontent.com/taMEA5xlCYQ-oA1vhova_W0QFgZC8cLu2yavZPucn9Wt9c6rnPuCqZwJD6YuTGtYI8RXS1rgvZlzs7ndOC57DVkzKOtYMcACrNU2tCbc7lI_tq7Y6fCCDh2WtkDv622wKglzn8QiOirx43vsZg)

If you do not see the icon as shown in the image above, please check the region and ensure that you are in the _N. Virginia_ region.

26. Close out the welcome pop up.

![](https://lh5.googleusercontent.com/xKRj8zULWZouUYTzXEuYkxGHgp1On1BuSxagxKI2c0hv7YY2cgDUzXa5Pis3nrFF1ZZqG-jnmpnB9b0nbkcZwW4b-6HiB3KjI4JMbHO5bf-clM9HnrYhQv12LZXSP9kW3cCd4c3z5kJJOuBfFw)

It takes around a minute for cloudshell to launch and to get the prompt as shown in the example below.

27. After the cloudshell is launched, we will first ensure that the home directory is empty by running the below command.

```
rm -rf \*
```

28. We will then start by cloning the following github repository:

```
git clone https://github.com/PaloAltoNetworks/lab-aws-cn-series-zero-trust.git
```

![](https://lh6.googleusercontent.com/KTFszTOkh3NyoBLfdzZPoI8eXqwdpalZ_xe7l41XgNO0u7q0KKQaGAgDBwwYsF2nLZ6Ps77BrF7tgpm5UjoQlmpGto9aV3mplTAb_GwBM9Hj1oRMIkjYr_FJnbf3xsZQuY4maGd3XpLne2IeIg)

**Figure:** Example of cloning the GitHub repository

29. Change current directory to git repositories’ root directory:

```
cd lab-aws-cn-series-zero-trust
```

30. Run the setup script:

```
./setup.sh
```

It will take sometime (**~10 mins**) to deploy all the lab components. Status will be updated on the cloudshell console as deployment progresses. At the end of deployment, you should see the message “Completed successfully!”

![](https://lh6.googleusercontent.com/8EZTut_ydtGxXEiPA3JtPD3J1Vvu3N-KUtv7n-fNRweUhFkguWJ3nGVz0Ljns6fo7Rst8sQsfdSnh4b7pkJAH9oKJOg8wFg_QyxIWT5ZkhGyLhSD6I5WbRn9S1fbCn3HK7COQ2uxquudjIzB_g)

**Figure:** Completion message of the Lab Setup script

31. Make a note of the “eks_cluster_endpoint” value as shown in the figure above. This will be used for configuring the Kubernetes Plugin on Panorama at a later step.
32. Review the deployed lab environment with the topology diagram shown below.

![](https://lh5.googleusercontent.com/u4dfV5cKDaJskw8OC19h-Pbt_owHTUBfBiDvnx0RjQbldrrLbV4f0ccHB2Mn4_oUGN43Dng-HYV_EZ1_KUZ4qK5RBGnaX7ulL5DPmlp6ediuXzoFSOf044K1z71v51EFPCKWhGRf3Vb-fXa9oGo)

**Figure**: The network topology deployed for the CN-Series lab

33. On the AWS Console, on the search bar at the top, type EKS and select _Clusters_ from the listed results. For ease of use, open the same on a New Tab, so that we can continue to use CloudShell on the existing tab.

![](https://lh6.googleusercontent.com/h6F4TYuDFvnVAomaZvza2X6ztgu0x3SQJ8-yNejG7wxkQz5aauWK1XDLZ4uelCGicvUqJtAFNTJtfiks6IlZlUNTDnp-ykJOMZVqFKl6_OzTGu3FDEoAFaZsCW0LTASs0uIFna1XX8fsInlvNw)

34. Review the EKS Cluster that was created.

![](https://lh3.googleusercontent.com/9unyCvRErA8vEYPQhjME-qGA2iN1GUZWUuNxkA2iS6bJVMzOS0GY8opzpNoz7Ilrfa2TxXvFKfQI-FXHBAYp3QrvKPzYyZxsgRziajBVDONcT7hpxqwZ2riu9wWXjuWIDP56CB5SjXiuG7Q5Yg)


## Deploy CN-Series firewalls and the Application

Before deploying the CN-Series firewalls, we need to configure the public IP address on Panorama.

35. On the CloudShell tab, run the following commands. Note the Panorama public IP address.

```
cd ~/lab-aws-cn-series-zero-trust/terraform/panorama
```

```
terraform output
```

![](https://lh4.googleusercontent.com/OPqvqUKXa4LggAmbPqDs5nWfglyOEW6ymxZAfghPRnQ2p1AdlbbLWB7u6aSLovEi21R-3ch6HZc-Ct_1SLp5rPmEBCOfsY4WTxU6nhPY4_ydKrl9hRYuffVqajYZuJsYQBkJfP0XNDz94EpsWg)

36. Open a New Tab on the browser and open the Panorama console using the IP address noted in the previous step. Make sure to add “https&#x3A;//” before the IP address.

![](https://lh5.googleusercontent.com/wNNiWcsQvEEAUJK7qEMaNwqIfXVcgo_32CzAfIi_CScIJqAgdba9jqX8QL_fUMVDoYmp6VsxXIa5l9VA4aK0fBq0LAUn_HyNlRbOCxOmyr2LT0WdesBpwCDPHnMTOcz7xhLL27uOiJHJZ0EKWg)

37. Log in to Panorama management console:

|              |            |
| ------------ | ---------- |
| **Username** | admin      |
| **Password** | Paloalto@1 |

**![](https://lh6.googleusercontent.com/J6yaI2jqtWM97G5LamHF2OOf2AX8nBw5BsLLUQnpsrHY8be3VzxmwjVnHool4M1dzsJj_iVkuKh5zgJdyD4yKq1aIgKAv4JFlQbRhMJkOi2teH7MpZMTe780R1ixyh4RbX19s8EKKIY-_3OuDA)**

38. Once you have logged in, navigate to Panorama > Setup > Interfaces, as shown in the figure below.

![](https://lh5.googleusercontent.com/tlunSvuI3hN4hufTya9SvIUkS7-40HWRor9B_ziPWiu59hr0hIhHTJjcaXDGobZ83PdxPa5LeR7T-sI7lMcj_op-moK51m9MiQB2hnkvWK9F1Sbr0qm20BuHHNnIS5WGnK_Z2stzEfqT3syXqQ)

39. On the Management popup, enter the public IP address of Panorama as noted before and Click OK.

![](https://lh5.googleusercontent.com/tbZhmA29DiXYvzZdKKXdW6TcYZKLirRh2r1aAzf0_gR-kNxM-tXL7QQGt5CShZ_iVz2khytRYtyc-VzOqzP3q8L5lnZsa6kpAckI7pwpjJp4EYbW0DJqtIcHRkRd0Mg1wQJnMXWnyPtT2mn41w)

40. On the top-right side of the page, locate and click on the “Commit” dropdown list and select Commit to Panorama.

![](https://lh4.googleusercontent.com/rUvh2mkbsaxFk95zpSXalTHAPAuMgzqR_pBW3U3rKNxH5M_2OQG8DliyrXQxlJQSwAnCZ3MRCiacQws-UNOUbwF2dGRcBzUwaf25bbzPeXYPmlXUfe2Hf-2ZFiOqMt9aR3O4Lm_IIZ5sqFWv_g)

41. Navigate back to the CloudShell tab and run the below commands. These commands are to deploy the CN-Series firewalls.

```
cd ~/lab-aws-cn-series-zero-trust/terraform/cnseries/cn-series
```

```
./install-cn.sh
```

![](https://lh4.googleusercontent.com/dew2qNmWTTeMQtMdlquFp8fi5Mt5qEUyAtsZCrFUX3Ifv9dl7xN1bRGA_p7tM1xLfJMJ3nfzOzo885281Gpd-kiJA5gZWmVsRk5N1W_J9hrGLBjIlEgSOkwY8e67jXmS4NOHk6qNDUgJQDpJ9g)

42. Now, deploy the sample application by running the below commands.

```
cd ~/lab-aws-cn-series-zero-trust/terraform/cnseries
```

```
kubectl apply -f ./sample-app/guestbook.yml
```

The deployment of the pods for both the CN-Series and the Sample Application will take **around 10 mins** to complete. During this time, the deployed CN-Series firewalls will attach themselves to the Panorama as well.

We can review the status of the pods by running the below commands.

For CN-Series,

```
kubectl get pods -n kube-system
```

![](https://lh3.googleusercontent.com/UbBfv2qIDRGbqaY7WL8dHgULDqMsyAkGSu_jZTED1QWDE5I-TULaxESCNAhWiUqkSAUfXQMtVs0qprtCIAAAm2xTSt8a9TmNMEkYUGMu4IqxsdxGiVQ3blnZb8SIbIjLaXpxQHC6ffcj0-ygGQ)

For the sample application,

```
kubectl get pods -n sample-app
```

![](https://lh5.googleusercontent.com/D8K0DBB9gm97rLOV81u3xNAkbM_Lon_mXKM7ta13IFGx8PExhNCdjvTBEG7KTxQtzJ1QGeWODd6_4yO0B4jxmscey3qXR-AQzqpdfY6atXrQsZsarfNt7zjSmo5dWtB2MjuTkbxulURdMDXRpw)

43. As seen on the images above, under the READY column, all pods should be **1/1**, and under the STATUS column, all pods should be **Running**.
44. Once all the pods are up and running, navigate to the tab with the Panorama console and on the console, navigate to Panorama > Managed Devices > Summary. Note that the CN-Series firewalls were added through bootstrapping.

![](https://lh4.googleusercontent.com/68KYMoLA3W-EnVE6MCFb_gmhI_15YglopVtjewwMt7Kogf6m1iYYwr4HJu34Vv-fMoQHWBd7Sr_qq5hq_-W2475dQF3Vn_mlBi88hAlqlW2iS1WCTRIMdRQbNQFezLHFokYq61Tl-_JhakTNJA)


## Configure the Kubernetes plugin

45. On the CloudShell tab, run the below commands.

```
MY_TOKEN=`kubectl get serviceaccounts pan-plugin-user -n kube-system -o jsonpath='{.secrets\[0].name}'`
```

```
kubectl get secret $MY_TOKEN -n kube-system -o json > ~/pan-plugin-user.json
```

This will create a credentials file to be used while adding the Kubernetes cluster in Panorama.

46. Download the file by locating and clicking on the “Actions” dropdown list on the top-right side of the console.

![](https://lh5.googleusercontent.com/U0dqeL70RWEPjvhM3fiw0AiOwmKCp3rFB7fLr0FuA45SxG_8C6l5dBoXdRQRW-poJa5mnn3AUCRh_crZAwutzqjM1MIy--H8GgeSs3PksxEL2LBMXPdymAug7v50-MOOXy9NlN0BXCZYqek02Q)

47. In the Download File popup, enter the following path in the text field and click on Download. This will download the given file into the Downloads folder of your system.

```
/home/cloudshell-user/pan-plugin-user.json
```

48. Now, we need to also get the EKS API Server Endpoint. Run the below command to change the directory and get the value generated by Terraform.

```
cd ~/lab-aws-cn-series-zero-trust/terraform/cnseries/
```

```
terraform output eks_cluster_endpoint
```

![](https://lh5.googleusercontent.com/YsH4e-ppDQZepX6XHZwWNgYKga78tGVvGy3DXIPQ2QMfTuzw0SXkmZ7NIHxnmeN-jVY8Oyie3rfS0c3Sao2QW5-g91s3U8kiK2TjV-RB3MHEhZXi_pUIeA-mBkTEYY5JxoFTMhKgaD7_3ngDHw)

49. Make a note of the value, you will use this when asked for the API Server Endpoint while configuring the Kubernetes Plugin.
50. On the Panorama console, navigate to Panorama > Kubernetes > Setup > Cluster and click Add.

![](https://lh6.googleusercontent.com/bSucOG0yCkA8pIA3_EpX0CDHR0_eRqZTxLo9mo49X1eE4Y0RyV9B42ofO_A9EBGvL1r-8BtZ2ikFumZ1t6EKZWl-1_MJD98rV1hwdI7mFiiKHKDDRz4H-dPnu91dxqwQKrxNxf-RsbhaO6ApTA)

51. Enter the fields as given below.

    1. **Name** – k8s_cluster
    2. **API Server Address** – Use the &lt;eks_cluster_endpoint> value copied from the previous step.
    3. **Type** – EKS
    4. **Credentials** – Click on Credentials. Browse to the Downloads folder that contains the pan-plugin-user.json file that was downloaded in the previous step.
    5. **Label Filter** – “Select All Labels”.
    6. Click on **Validate,** to ensure that things are in order.
    7. Click on **OK**.

![](https://lh4.googleusercontent.com/elsT0oH5vHOcjGSPTR4abRWubdG1x9eYQl6V_LbFJzCAuqgLPaTwipN5FNP72cewHUMjqvW4zG30TqXqC_DhnC3cvhtd5vpG6ihBsx-5LgpJ9rTs4b5YR392E07l5zEws6Ubf06Pi_nbnP61KA)

52. Configure ‘Monitoring’ by selecting the **Notify Group **tab, click **Add** to add Notify Group.  Setting up a Notify Group will allow you to segment which Device Group receives notification for changes to a given cluster.  This allows for very granular rules.

![](https://lh6.googleusercontent.com/5M6HnbPmcp7FPHHEuTG8X_bSvIZcGzlyPwIy_YzJGi8_6Hx_0Aby9KsbFzdWgksMfv6s7wgttAbZyjDx2ftRkDsVwsVe6ymxY6JOSaI_gEE37u5MCk-t6awaCJW-hgECYllHmx-QASQpbHkpYw)

1. **Name**: k8s-notify-group
2. **Enable sharing internal tags with Device Groups**: Check
3. **Select Device Group**: cnseries
4. Click **OK**.

![](https://lh6.googleusercontent.com/k5M897JkKxuI4Tyr7jlOyGTtK9kH1EAYoIPuQBf6LdclzedsYnr6t313aDrkh3XVDkvvv23O75u-20Oev-a3IAjYhZrPgNR2ts8vwKwqSrDbwrHt_7HYLyGnr-2dX_TJaD1wXgp4gAqAI7W1-Q)

53.   Now configure the Monitoring Definition and specify the cluster you created in the previous step. Navigate to Kubernetes > Monitoring Definition > Add.  Fill out the Monitoring Definition form:

- **Name**: k8s-monitoring-definition
- **Description**: k8s-monitoring-definition
- **Cluster**: k8s-cluster
- **Notify Group**: k8s-notify-group
- **Enable**: Check

Click **OK**.

![](https://lh6.googleusercontent.com/x7TbpEeU81YzO-I_vSi9oMY9xskbB48jOmwzmderSfEhbxvHi5Elq92UaO_oFiY-HmuZIbJPkiyaVgsszMtvqpOz6XVR83eot04oBNQ1vVnEyZz8nkpuwbI9JTN_kmRRZxJ6Cx5Bs4CWghBAKA)

54. Now that you have created the Monitoring Definition, you can see that the status is Initializing.

![](https://lh5.googleusercontent.com/tgCjHuUO1su-tf3JsyKAH5kjtu6_R5qjexdDGre4FAaJsaXVMkPUxAd6in6gZ0MUP3-sMGFCqTohon7ocwdkSCGv3nCFSF3muPu8f8I5lF4X-w7jtcQSD7V_ih8-7oY2CSZr4LHxqER7EZ95DKw)

55.   You need to Commit and Push the configuration. In the upper right corner select the Commit Icon then choose Commit and Push. 

![](https://lh6.googleusercontent.com/cYdKWmGgogzMjkPl5jj2oKOpvWhilPc8lL63W3DQBua3sbHVVpko8uM4BiERWVolIg1ml9VwCt5mXMwiNoM_fcEApQbHx8ncCj4b766aYA3idZIQUR7GANW7XXlq1ukB8J7EwZ-DOIj-AIqWFA)

56. In the “Commit and Push” popup, Click on **Edit Selections**.

![](https://lh5.googleusercontent.com/V0Q9R2TAEnI6zoh5qfl4bxyEPDbmWZHalQ_UXmhtg3o5sdLD41VCVa6I1VzI29q0IT4SFNMZ1kwVnAZoqWQp5tIsxK1hl-JPW_4F_h2PEViZcbdSzhlcCjxzLIl8DosUPJl-AD_vKAEL2_97P6s)

57. On the **Device Groups** tab on the popup, check the checkbox against the _cnseries_ device group.

![](https://lh4.googleusercontent.com/eJ35TMLcyCBZssd3a94fUmNEdTnxgPM7LkPtVfyYTlLrIIx4rQSIVGj4lhbBGlimqg4AI42V3YaIiTNeZ5aXKZRaJ9Q6ENg4ClKY0HG0pEA3jrA-3xgvKjuwPr0wXusEsofNjNqrjQasOrhwN8Y)

58. Navigate to the **Collector Groups** tab in the same popup and check the checkbox against _panorama_.
59. Click **OK**.

![](https://lh4.googleusercontent.com/JP1yS44HgHVkmzBA4tu_Xivn9OjgouyekGKNADuQoAtg8LGX9ybsrH-Ur59-FwNFuDTY6uPSYLbXnEaV0T-ExadD19f5U11KHGsNvWLP2c3U_4klOyqSEvtr6ZmsUKK25JWLa04lGH3SjneYfzI)

60. Check **Tasks** to confirm all jobs are completed.

![](https://lh6.googleusercontent.com/TSrAbUxGPNHD8nRuWzGOSqesyexM_EKZFMRCyB5WlDzimOkLkaEqX3B88haTbRfFXo7hMKIl3DdEVXOBo_OxvugHlHxOkQaXHXPfHsHyve21t6CSdK9hcrRf35QUv7IDgLu3RQXZti80XRn-lw)

61. Once the commit is completed, check the status of the newly create Monitoring Definition, _k8s-monitoring-definition_. The Status should say ‘Polling Connected’
62. Click on Dashboard

![](https://lh4.googleusercontent.com/PG_K7PnxCy5I7m_8iRbbprsvKP8FHAiat9Nf1hjPhnORExOSINLGQDPgCT6V1Bu5Cgh8XaRN3RFrDDATJMComKsF01Sgtsoy1O2kC0l51wpNOKuSMXqnOLhq98qVEFgISb5DBuV-bzBaJAjClg)

63. You can now see that the Panorama Kubernetes plugin has connected with your kubernetes environment and synchronized the kubernetes tags.

![](https://lh5.googleusercontent.com/6owmDhw2XtwWZGBJIDFC1UVfjgpwB_DfL--_VN-fdL9aslirxEEJmcGyNo-2tJ0h9fsrqriRBR03bhrq40PdxV62JwbtsIhWFeE69Kk6bdh8GqKOu5eS0BywTdgBf5tADWka79wS6jv_pUWTkw)


# Activity 1: Protect Against Log4j Attack

To secure your containerized application you need to be able to visualize and control the traffic between your pods. Plato Alto CN series firewall allows you to granularly control this traffic.

In step 39 of the previous activity we deployed a ‘Guestbook’ application.The ‘Guestbook’ application a 2-tier simple redis application with a frontend and backend tier. The backend tier will consist of a **_redis-master_** and **_redis-slave_** for db redundancy. Even though there are two tiers in the application, only one (the frontend service) is exposed to the outside world via a load balancer. 

First we would see how having a CN series container Firewall inside your K8s environment gives you visibility to your inter-pod traffic. Then you will use the granular controls using kubernetes tags to control that traffic.


## Activity 1a - Gain Visibility on inter-pod traffic

64. On the Panorama tab on your browser, navigate to ‘Policies’ and select the _cnseries_ **Device Group**.

![](https://lh4.googleusercontent.com/fUAMBBgerzCNWWkMYCoRxlRtwHyJgeEc1G9ddekRhNRlX1dMbzL6osvHWXC1CGm48m58i3zMABrqf8McWHMTCcbcLhOyTG7iurOl7ISFy7ePJCtLlSnf-vI1b3Mr7UWuh4zRzdiYoBarg0R_5Q)

65. Review the policies. There is an allow-all policy that will allow access to all traffic.
66. Access the web frontend of the two tier application. On the cloudshell window execute the command below.

```
kubectl get services -n sample-app
```

![](https://lh4.googleusercontent.com/BRLys3BumHDf774UOcUAzsILH5UsOdSc0pQq-T3jZrJHZOGO18nye7GaWPk3A6cZ0J_syMLNw_7wXdW9oxVBWv8PCktuwjJZNHOnidJ7UQyC1vrNTXeZ0ExavFbkIWWgPraSk4SF7YbDGRhGmQ)

67. Copy the URl to a new browser tab and enter.

![](https://lh3.googleusercontent.com/kzAC8OBRp5U1wPKbC57SnbfpCfjWj2yZnGc-ptzgAvGY7xpLpP_to2hAUlwpMk4PfS4nIFEyICV6Ln2xTH7O11opJyIeX3evjai7L26fYhfQckFY2E7oksMUilXESQwm3uHSRV09A272TK-rFg)

68. Enter ‘Hello World’ on the ‘Messages’ tab  and Click Submit

![](https://lh4.googleusercontent.com/0yhjZWN9M1VyEVYG_rHhL7r0a4E79zHp4O9wvyz8ZEYjtuJuYlxzchnB5rVLv6evxduXPnsw9JmWsx69jqYHp5wDw3bDTuFi1u6NWq93s96ggFmYDmofxC1Mb7XqWPQVCII_Gtb9PS4fLDb8eg)

69. Guestbook app saves you message in the back end database and prints it back on the webpage.

![](https://lh5.googleusercontent.com/tg34Wh9zUaITgI8Xx-T5oIQssS_RBKiRzDMNBBYQNmOV8xGwc6loAuZdJ2I_XhSFy-GCC8pS2dxEiUfoubLGJqiMhHNGgOIKXd06uu_Nr8RJ2KQX2deVCzwGVi__cdCItFiL-lDNPGFoa5R0Jg)

70. Navigate back to Panorama and select the **Monitor** tab. Under traffic log you can now gain visibility into the communication between the Web Frontend pod and the Backend Database. Note that the CN-Series firewall identifies the Layer 7 application as the ‘Redis’ database application.

![](https://lh5.googleusercontent.com/Ck2UePfXkPklNDYcf8N5xesDLIi5U6BptVTGKO0TnvCKxQHivdCGQoxs_RgA1nXdekVoPvgA84lyCT-KOpcxIL2nIvT_7R0S1Qrxj4NyTJKa4LdmWza4q0RDhXgo6tRpZ9H3TmgsNdph5pfbOg)


## Activity 1b- Granular control of Inter-pod Traffic

In this section we will create granular policies on K8s tags and use the policies on CNseries container FW to control interpod traffic

71. Navigate to ‘Objects’ tab on Panorama and locate ‘Address Groups’ on the vertical bar and click on Add button at the bottom of the screen

![](https://lh5.googleusercontent.com/N-JxwW_8Qnbulzkb6OOjI7_XIsIsx3O2MNSZKBi3RllhJqbX7VsoAP40H2qhs4snZpI6zWFikQe8EuZj84cg4u3Gd-VBp25kjIYbY3vCPvVccMeNgrpZfVPOYBIleCjR1t9QVBZ88P-wY68TVQ)

72. Name the object ‘Frontend’ and select Type as ‘Dynamic’

![](https://lh5.googleusercontent.com/xGzuP-auk4jLFp6MOEhBatlpH2JLZvJ4hnhikhx7H1GhaVnU_8QhPsjYBD8D_P9Q-yk1WFmrGzf5n4vh8MCFcjV0OZ-uw9YOlC51Ddue-IP0fFQ6jfmw9iVsxm6iyYhaoinPRX8EqMG1HGD5Gg)

73. Click on the **Add Match Criteria** button. This brings up a window that lists all the K8S tags learned from the K8S environment.

![](https://lh6.googleusercontent.com/oxBPoFYtl2bTwyZ8mcMiKCbPVyoCh9IS-YEYlanbe5GUrBVauuZCjk6AD746C9PFyHiskJL9t2AG1auiw1fESGD5cl2RV7KqeQCBjovhZhHevcCM7QvvuwQlJ4XdDdwGrClJhkLYeu4d1b46Ew)

74. Now we will  define the match criteria to match all tags that have the frontend string. Select “**OR**”. Type in **frontend** in the filter and click on the → button.

![](https://lh4.googleusercontent.com/n8faFA9nfGI8g175Y274YdRL2vm9CvE2MNRFCP1MYUUg4K0uGe_72aOW2s--EzAfw-rUBIVubNHKDHJG5156qBd6smhq3CxsHUCjRA41D8F1kq5x3Xbq1YKQOFp8CaUTQb8yur_XWxfMRgGj-g)

75. Click on the + button against each of the tags to add them to match criteria.
76. Click on **OK** to create the DAG.

![](https://lh5.googleusercontent.com/e5bmyp-W2VvssTE01BCbPTisjuAI9dAIf3Cf3dgVI5D0mWpldb2wb46kBLkOumAEqg3X9-hEeBDAuMqUeuXLtviwPYan9i-MqVQrJ4WfzKca8ARbXL5_ihFwiUPVQyAhRLJ5089p-W3HEkYTdQ)

77. Now that we have created a ‘Dynamic Address Group’ for the web Frontend, let's create a second one for the Backend Database. Click on **Add** button

![](https://lh6.googleusercontent.com/-sO84yxOoMDklIVItL1EAW76lfITNuFiN5mPfAofx82KYEfwtwycz_taFN9uCz45wi50nEa1dLJ8UYNNMZ64PwTk3IvhpK5IbxeuTansWX16FEmi9KjPGxNF_NYFlclkng3mZkY13puqNWb3nA)

78. Name the object ‘Backend’. Click on **Add Match criteria**. Select **OR**. Type in “**redis**” on the filter and click →.

![](https://lh6.googleusercontent.com/92dvkROEGT2rA82pJXGF29NEigiu_Rl0YcjHwna7rW049xY1NDFJ0rtj0Bdh18eaGZOVbvC7XLurHJVnnczSC7_Ou5-hO82sNN3wQzLXqjZE_2HK-CgEmohE5-mrDOrwFbAeuT5B9aHa0Fb2LQ)

79. Select all the tags and click on **OK**.

![](https://lh5.googleusercontent.com/DoNLsWT667fctyeHj3BGrKIN88ii3j4xwa1zCP2oPKG0gT1gQSqjZUHoEYjiPTkO5BY-igNDfA5Uh-XjdbpsNwXh4etWEGk0Qug5V209pN_Gg42UJGlEzYAiCzfflzAfg9TA9LWo31M1HTY_Rw)

80. Navigate to the **Policies **tab. We will now use the DAGs to define policy to control traffic from Frontend and backend Pods. Select the first rule by clicking on ‘1’. Click on the **Enable** button to enable the policy.

![](https://lh5.googleusercontent.com/9vH29CtifGIlMjTn3_jETwug6PzmtEPfs9ypJ7y3Xw_k3ETLQM_LweXlv5u07LF8FJ_wKpgrc9XFYBIlt4i9IPYIHa_DLPb6EU_RlOYX6MxjokSrzkXE_J2IYwt-T1xF4bLgraGBuew49QNuqQ)

81. Click on the policy name to edit the policy

![](https://lh6.googleusercontent.com/emlwwdjlosY20ps3ZJ9kZC98Ex5Jh0GWJmcPkaxpqD2L5uSiKrmvWT87l85uLTwcMd3tAIUr3euqigu25vKXm2Vj6geHd430lKRgbk0PrvhMeA1yPvXhz2o0Z9DopVURW_xhhotQhmjypROivw)

82. Navigate to the Source tab. On Source address click on ‘+’ and select ‘Frontend’ from the object drop down.

![](https://lh4.googleusercontent.com/iP3jwAcJpO2nvY1TbM_NBroEKkjXs_gyaHIRA_ldwNDpGoOOmwcdXp7ffoTBZWf5O1Bg4mCRXek5UrriZqyEhkbxHA_g1WrsseVGyejTKUED9P58ngDzAl-rw68JsLufId_ZJVfFRIAVlaKISA)

83. Navigate to the Destination tab and follow the same method to select ‘Backend’ as destination.

![](https://lh4.googleusercontent.com/ta6mJG8BF6iSuphPQk7926IlNSOn73_mHYwmJN0EgOUzXFtUx-gE0iQ-7yuEJ1rRaoYpgNmuz2KbcskNN5px0IitMlfWFWJ5EtDu5JniEziLgxgInfi-SNVve-zMrBy5JDmfyRiyfn3JJuOfxQ)

84. Navigate to the Application tab. Click on the ‘+’ button, on the search bar type in ‘redis’ and select the application ‘_redis_’ from the list.

![](https://lh6.googleusercontent.com/_hxvnk4xpj2qUGJa84At7Oe5nu8lg0a1d3YdGOB7OHqzugtNY1Kudy8viDcIQzu9KMUIT0_NT9PPQ5mdUSSsjOAI74xqrtNlJcIVZDBr1yVZI6RGDoxmhWyEddrkmgfUiFnB7aPybVdBoYpxbQ)

85. Navigate to the ‘Action’ tab. Ensure that the Action is ‘Deny’. Click on **OK** to save the policy.

![](https://lh3.googleusercontent.com/zTrv98NHBloa4cv96aUqMCITkUkcAyLOZDFgusLK5xSPE7ZJtwx2kv1COAN69F5cqJF3a63x7zuFkGk5FeQo0lahQOKK5zznvHN72vzoSvZBm7qYR8DzI40e_bXCdvvsObbJW9ySGdT0NTXQWg)

86. Commit and Push

![](https://lh4.googleusercontent.com/6_9D_4pwjCWR0ywbwXj0fX_1QvkBqHQc0lWF1igZlI9u8qQhnB5VPsBvRP1zCK7AalZoBkVmA7jOkyKrvkBl-pWcCD1SuAHrjn4TmWiZkciHLotOUxlUi54ov_U_O_NhTa2ilxxyF3OQgKiTxg)

87. Ensure _cnseries_ is in the push scope and click on ‘Commit and Push’.![](https://lh4.googleusercontent.com/8ZgMGXgpLWVVB9-Z4YN8X_ttZ1BXZT8fqMTNmjh_0AR22n3ZVa8RPb6kS0lHxNLMu2bCY1y7uXbj9YG8gBW0linE2y1YNlPyXkJAR4x_TgWa-s1bzyOtXIYauLiguXD0xxlieaSuRuRcGSCJ5Q)
88. Wait for all tasks to complete.
89. Navigate to the tab where the frontend web page for the guestbook app is open. Refresh the page.
90. Type in ‘Hello World Again’ on the message tab and click submit.

![](https://lh5.googleusercontent.com/bf_-IoIXIBtAcebZiLXPIduZSoiSaOPJeyl4zKnpZB_DY1zpkJ0VXI9JgbmI-J8NHsx_DhTkqd9CyRN2Yk2kucqCDl8pXzXzN9h6hUT3yPfhKnsPIHJqc9bT95QQDy632dxwxNFge756GJKiAA)

91. You will see that this time the application will not echo back the message;
92. Open the Panorama tab on the Browser and navigate to the Monitor tab and visualize the traffic log corresponding to the firewall policy now blocking the redis application between Frontend pod and the Backend pod of your two tier container application.

![](https://lh3.googleusercontent.com/k4o2yhWxFde2Krsqv_XvS-OqArnkVdacMIl0vi7Mwid23qwivUN9nR-XoNDbvPtrA8yhVDjt34aWhtJ8NnT0pEISR7CGDze6GJS-VUh3pLJtK3yrpyuF1W3qYBc2lcdL1NykqNO9oElPKWzB-g)


# Conclusion

As we conclude the exercise, you have familiarized yourself with the basics of EKS (Elastic Kubernetes Service) on AWS, deployed a simple application and secured the network communication between the pods in the deployment using Palo Alto Networks CN-Series appliance.
