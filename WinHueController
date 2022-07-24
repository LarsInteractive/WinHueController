# example: python winHueController.py -ip 192.168.100.1 -user 123DUMMYDUMMY456 -group "Living Room" -scene "Chill" -action on

import argparse
from phue import Bridge

parser=argparse.ArgumentParser()
parser.add_argument('-ip', action='store', help='ip of the bridge', required=True)
parser.add_argument('-user', action='store', help='automatic generated user of the Hue Bridge; if newbridge is used, enter None', required=True)
parser.add_argument('-groupname', action='store', required=True, help='group to control')
parser.add_argument('-scene', action='store', required=True, help='scene to show or None if you  turn off')
parser.add_argument('-action', action='store', choices=['on', 'change', 'off'], default='off', help='switch group on; switch group off; change scene, only when light is on')
parser.add_argument('-newbridge', action='store', choices=['yes', 'no'], default='no', help='use yes when the bridge is controlled for the first time')

# If the app is not registered and the button is not pressed, press the button and call connect() (this only needs to be run a single time)
#b.connect()

args = parser.parse_args()

ip = args.ip
user = args.user
groupname = args.groupname
scene = args.scene
action = args.action
newbridge = args.newbridge

#------------------------------------------------------

if newbridge == 'yes':
    b = Bridge(ip, None)
    b.connect()
    b.get_api()
    print('Bridge connected')


b = Bridge(ip, user)

# Get the bridge state (This returns the full dictionary that you can explore)
b.get_api()

if action == 'on':
    b.run_scene(groupname, scene)

elif action == 'off':    
    b.set_group(groupname, 'on', False)

elif action == 'change':
    
    groups= b.get_group()
    for id in groups:
        group = (groups[id])
        if group['name'] == groupname and group['state']['any_on'] == True:            
            b.run_scene(groupname, scene)
            break
