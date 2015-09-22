# QML-Network

A QML wrapper for c++ Network class with loading functionality and optional token variable
This is just a quick implementation, so make sure to double check the code before using it in production

a quick example 

Item{
  width: 100
  height: 100
    Network{
        id: mynetwork 
        token: "abc23kljsdasdfasfasdf34kldks" //optional
        anchors.fill: parent
        onNetworkReply: {
            console.debug("got network reply")
            var j = JSON.parse(network_reply_string);
            if(j["status"]==true){
               console.debug("true status")
            }
            else{
                if(j["error"]=="Token not found"){
                    console.debug("contain the wrong token, will delete it now")
                }
            }
        }
        onNetworkSend: {
            console.debug("signing in in network with token")
        }
    }
    
    MouseArea{
      anchors.fill: parent
      onClicked:{
        mynetwork.addParam("comment","This is my comment")
        mynetwork.addParam("title", "this is my title")
        mynetwork.sendPostRequest("http://mydomain.something/commenting")
      }
    }
  }
