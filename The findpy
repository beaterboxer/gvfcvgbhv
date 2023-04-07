import requests, random, threading
from colorama import Fore
class stat():
    i = 1
def check():
    num = random.randint(1000000, 17500000)
    proxy = random.choice(open('proxies.txt', 'r').read().splitlines())
    proxies = {'http': f'http://{proxy}', 'https': f'http://{proxy}'}
    headers = {
        'authority': 'groups.roblox.com',
        'accept': 'application/json, text/plain, */*',
        'accept-language': 'es,es-ES;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6',
        'origin': 'https://www.roblox.com',
        'referer': 'https://www.roblox.com/',
        'sec-ch-ua': '"Microsoft Edge";v="111", "Not(A:Brand";v="8", "Chromium";v="111"',
        'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36 Edg/111.0.1661.62',
    }
    try:
        response = requests.get(f'https://groups.roblox.com/v1/groups/{num}', headers=headers, proxies=proxies)
        if "Too many requests" in response.text:
            print(f"{Fore.YELLOW}Proxy Limited: {proxy}")
            return
        try:
            owner = response.json()['owner']['username']
            print(f"{Fore.RED}Group with owner  Id:{response.json()['id']} | Owner: {owner} | {stat.i}")
        except:
            if "Group is invalid or does not exist." in response.text:
                print(f"{Fore.RED}Group invalid {num}")
                return
            if "isLocked" in response.text:
                if response.json()['isLocked'] == True:
                    print(f"{Fore.YELLOW}Locked Group: {response.json()['id']} | {stat.i}")
                    return
            else:
                if response.json()['publicEntryAllowed'] == True:
                    with open("Open_group.txt", "a+") as file:
                        file.write(f"{response.json()['id']}\n")
                        print(f"{Fore.GREEN}No owner found: {response.json()['id']} | Open {response.json()['publicEntryAllowed']} | {stat.i}")
                        return
                else:
                    if response.json()['publicEntryAllowed'] == False:
                        with open("Closed_group.txt", "a+") as file:
                            file.write(f"{response.json()['id']}\n")
                    print(f"{Fore.YELLOW}No owner found: {response.json()['id']} | Open {response.json()['publicEntryAllowed']} | {stat.i}")
                    return
    except:
        pass
    stat.i += 1
while True:
    threading.Thread(target=check).start()
