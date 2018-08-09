This project involves the development of Beyond 4G existing network in both Silicon Valley and New Delhi as well as the development of two new sites. The two new sites include Sydney and Beijing which require connectivity to other sites resources as well as a network design which is designed for scalability. The new network design will cover both existing and new requirements which are broken down into general requirements, application requirements, devices requirements and other. The new network design will aim to meet these specified requirements as provide flow analysis to clearly communicate the new network design. The report will include logical designs, physical designs of the existing and new network design and aim to provide all relevant information required by Beyond 4G.

### Document Purpose

The purpose of this document is to provide Beyond 4G a detailed look at the existing network and the improvements which have been made with the new network design. The document will provide requirement analysis, flow analysis, logical designs, physical designs, network addressing, security implementation, management, performance mechanisms which will be relevant too key technical and administrative staff at B4G. Flow charts are being used to show the development process of the network design as well as outlining all other network design changes. 

### Scope

In this section scope items of the network design are broken down broader items which is then used to clearly outline the functional requirements of Beyond 4G network design. 

1. Network design budget

   The network design must be within the budget if specified. 

2. Network Security

   Private & Public IP addressing.

   Implementation of best security practices

   Prevention of DOS and reconnaissance attacks. 

3. Network Infrastructure

   Device requirements

   Application requirements

4. Network Performance

   Quality of service – Video conferencing

5. Network Scalability

   Scalable IP addressing

   Scalable devices

   Scalable design

6. Network Deadlines

   Network design is completed within specified time frame. 

### Outside the Scope

In this section, out of scope items are listed to limit the design of unnecessary network features. 

1. Partner Companies

   Partner companies require remote access to B4G however, the network design for partner companies are outside our scope. 

2. Customer Information   

   Our network we require security for sensitive information for intellectual properties or even employee sensitive data.  However, we will not be designing a network to store customer sensitive  information. 

3. Staff Training 

   Training staff use different software and hardware will not be within our scope. This will be the reasonability of Beyond 4G. It will also be Beyond 4G to ensure staff are train on       appropriate security practices. 

### Assumptions

The following are some assumptions made prior to starting the project and during the design of the network. 

| ID Number | Description                                                  | Area                                                         |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **A1.**   | The network design must be designed   within the B4G’s budget. The budget is currently unspecified. | Network Design                                               |
| **A2.**   | The design of the network must be   completed within B4G’s specified time frame. Assumption is implementation to   be completed by 17th October 2016. | Network Design and Network Implementation                    |
| **A3.**   | Number of reception staff and computer in   New Delhi office’s. | Network Design and Network Scalability                       |
| **A4.**   | File and other resource sharing among   software developers, product engineers and hardware specialist at New Delhi   office’s. | Network Design and Network File Sharing.                     |
| **A5.**   | Collaborative application and   implementation into network design. | Network design and application   implementations.            |
| **A6.**   | The number of training staff in rotation   at the Sydney Office. | Network Scalability.                                         |
| **A7.**   | We assume that all building will be   fitted with CAT6e cabling. | Physical Cabling                                             |
| **A8.**   | Assume segmentation and authorization   requirements for external companies and office’s | Security, Network segmentation                               |
| **A9.**   | Assume that at both Sydney and Beijing   Office will have some sort of implementation setup for internet at each of   the sites. | Internet, Connectivity and segmentation.                     |
| **A10.**  | The connection from building to the ISP   routers is an assumption are we using a cable connection or Fiber   connectivity. As this may impact network performance. | Network, ISP, Network Performance.                           |
| **A11.**  | Network reliability needs to be over   99.9% because they need to share files or collaborate with employees at   different sites who may be in different sites. | Backup links, network resilience, network   reliability and VPN connectivity. |
| **A12.**  | Assume that Beyond 4G is responsible for   training their own staff and that we will not be responsible for implementing   any training strategy or plan. | Training staff should focus on security   practices and if needed software and hardware use. |

 Requirements Analysis of Existing Network

This section of the report will focus on the requirement analysis for the existing network. The requirement analysis will cover both Silicon Valley sites and New Delhi sites. 

### Silicon Valley Headquarters 

| ID Number | Area               | Requirement                                                  | Importance  |
| --------- | ------------------ | ------------------------------------------------------------ | ----------- |
| **RA1.**  | General            | Finance, Accounting and Management need   access to shared resources and authentication must be used to access those   resources. | Recommended |
| **RA2.**  | Quality of Service | Dedicated video conferencing is required   for seminar rooms. Up to 20 devices all require network connectivity in   seminar rooms. | Required    |
| **RA3.**  | VPN                | Require remote access to external partner   companies and other location from Silicon Valley | Required    |
| **RA4.**  | Scalability        | Demonstration area requires wireless   connectivity for over 100 people at any given time. | Required    |
| **RA5.**  | Wireless           | Require wireless connectivity on all 3   floors of the Silicon Valley headquarters. | Required    |
| **RA6.**  | Backup             | Require network backup solutions in a   centralized location for research and development teams. | Recommended |
| **RA7.**  | Computing          | Servers on third floor can distribute   computational resources between themselves and multiprocessor computer’s. | Recommended |

 

### New Delhi Development Centre

| ID Number | Area               | Requirement                                                  | Importance  |
| --------- | ------------------ | ------------------------------------------------------------ | ----------- |
| **RA1.**  | Connectivity       | Require network connectivity for over 56   employees both wireless and physical connectivity. | Required    |
| **RA2.**  | Connectivity       | Require wireless connectivity on ground   floor and reception area. | Recommended |
| **RA3.**  | Connectivity       |                                                              |             |
| **RA4.**  | VPN                | Must be able to access remote servers are   Silicon Valley headquarters. | Required    |
| **RA5.**  | Security           | Require remote access authentication to   Silicon Valley headquarters when accessing sensitive files. | Required    |
| **RA6.**  | File Sharing       | Require file sharing amongst software   developers, product engineers and hardware specialist. | Recommended |
| **RA7.**  | Server             | Require data server possibly a NAS, and   other servers dedicated for computational tasks. | Required    |
| **RA8.**  | Quality of service | Meeting and presentation rooms may need   video conferencing abilities. | Recommended |

 Requirement Analysis of New Sites

In this section of the document we will be looking at some of the general requirements for the two new sites for Beyond 4G. The two sites are Sydney office and Beijing Office. 

### Sydney Office

| ID Number | Area                 | Requirement                                                  | Importance  |
| --------- | -------------------- | ------------------------------------------------------------ | ----------- |
| **RA1.**  | File Sharing         | Require file sharing between   administrative staff, sales staff and marketing teams. | Recommended |
| **RA2.**  | Security             | Require security and authentication   between various departments. | Recommended |
| **RA3.**  | Quality of Service   | Meeting room on 11th floor may   require video conferencing implementation. | Recommended |
| **RA4.**  | Network Connectivity | Require network connectivity across both   10th and 11th floors for both wireless and wired   access. | Required    |
| **RA5.**  | Testing              | Training staff may require limited access   to the network to limit risk of network issues. | Recommended |
| **RA6.**  | Scalability          | New office may require scalability   options for Beyond4G    | Required    |
| **RA7.**  | VPN                  | Require secure access to servers located   in New Delhi data center. | Required    |

 

### Beijing Office

| ID Number | Area               | Requirement                                                  | Importance  |
| --------- | ------------------ | ------------------------------------------------------------ | ----------- |
| **RA8.**  | File sharing       | Require file sharing between different   personnel for example sales staff sharing resources. | Recommended |
| **RA9.**  | VPN                | Require secure access to servers located   in New Delhi data center. | Required    |
| **RA10.** | Scalability        | Require network scalability for 5 people   over the next 3 years. | Required    |
| **RA11.** | Security           | Certain files may not need to be accessed   by every staff member, logging authentication is recommended. | Recommended |
| **RA12.** | Quality of Service | Possible implementation of video   conferencing for the meeting room. | Recommended |
| **RA13.** | Network exclusion  | Excluding training staff members from   certain aspects of the network. | Recommended |
| **RA14.** | Server             | Server room requires secure connectivity   with high bandwidth. | Required    |

 

 

 

### General User Requirements

In this section of the document we will covering the general user requirements which are applicable to both the existing a new network. These general user requirements are applicable to all users. 

**Timeliness**

Timeliness refers to the transfer or modify of information within a tolerable time frame. This is an essential requirement for all users at Beyond 4G as information must be accessible to each user in a tolerable time frame. If a user from New Delhi access files from Silicon Valley they must be able to access through files and retrieve them in a tolerable time. 

**Interactivity**

Interactivity focuses on response time from the system as well as the network. This is a user requirement that is applicable to all the users at Beyond 4G. As the response time to load or access internal network resources must be with a responsible amount of time. Round-trip delay is an effective way to measure the interactivity. 

**Reliability**

Reliability is also another user requirement which is applicable to all users at Beyond 4G. It refers to the user’s perspective of the consistency and availability of service. This is especially important for Beyond 4G users who require a consistent and available connection between the different sites. For example, users at new Delhi need to access resources at Silicon Valley. Due to the different time zones the resources at Silicon Valley must be available 24/7. This is achievable through backup links, secondary links, high bandwidth and backup servers. 

**Presentation Quality**

This is an essential user requirement for Beyond 4G as there are several meeting room and conference rooms which require high bandwidth to ensure a quality of service is delivered for audio and video applications. This is especially important for the videoconferencing rooms and as it is not specified what users will be using videoconferencing this user requirement is applicable to all users. 

**Adaptability**

Another user requirement for Beyond 4G is adaptability and the ability for the network to adjust for the demands of the user. The use of thin clients will allow for users to access resources stored on the server. This allows for users to become more mobile and make it easier for adjustments to new user requirements to be made. 

**Security**

All the users at Beyond 4G will be dealing with some sort of sensitive information. For example, research and development documents which is leaked could give competitors a competitive advantage. Therefore, a general requirement is ensuring all users have sufficient security implemented including integrity and authentication. Following good practices such as changing password every 30 days and ensuring authentication is required to access the network. 

**Affordability**

Another general requirement is affordability which refers to the ability to afford the cost for the new network architecture. Assumptions have been made on the user affordability requirements please refer to assumptions section. 

**Functionality**

Users at Beyond 4G may be using different application and the network must be able to support the functional requirements for each of those users. Functional requirements are tied down to the user applications which may vary user to user. 

**Supportability**

As Beyond 4G is an ever evolving company their future network needs and staff operations is likely to change. One crucial requirement is the ability for the network to support future needs of users including application and more. 

**Future Growth**

As beyond 4G develop and perform more research the user's application needs may change and the network must be able to grow and support new application and devices on the network. As it is difficult to predict the exact future growth estimates must be made.



Read my full report [here](https://drive.google.com/file/d/0B8_ultUvjADJeXEzbUEzelpxZ00/view).