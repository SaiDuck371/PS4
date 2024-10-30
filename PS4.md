```python
import urllib.request, urllib.parse, urllib.error
import json

serviceurl = 'https://bcferriesapi.ca/v2/capacity'

while True:
    ferry_name = input('Enter a ferry name (or press enter to exit): ')
    if len(ferry_name) < 1: break

    url = serviceurl  # Adjust if necessary

    print('Retrieving', url)
    try:
        uh = urllib.request.urlopen(url)
        data = uh.read().decode()
        print('Retrieved', len(data), 'characters')
        
        js = json.loads(data)
    except Exception as e:
        print(f"Error occurred: {e}")
        continue

    if not js:
        print("No data found.")
        continue

    # Print the structure of js to understand its format
    # print(json.dumps(js, indent=4))

    if 'routes' in js:
        for route in js['routes']:
            route_code = route.get('routeCode', 'N/A')
            from_terminal = route.get('fromTerminalCode', 'N/A')
            to_terminal = route.get('toTerminalCode', 'N/A')

            print(f"Route Code: {route_code} | From: {from_terminal} | To: {to_terminal}")

            # Accessing sailings for this route
            for sailing in route.get('sailings', []):
                time = sailing.get('time', 'N/A')
                vessel_name = sailing.get('vesselName', 'N/A')
                fill = sailing.get('fill', 'N/A')
                car_fill = sailing.get('carFill', 'N/A')
                sailing_status = sailing.get('sailingStatus', 'N/A')

                print(f"  Sailing Time: {time} | Vessel: {vessel_name} | Fill: {fill}% | Car Fill: {car_fill}% | Status: {sailing_status}")

            print("-" * 20)  # Separator between routes
    else:
        print("Unexpected JSON structure:", js)

        
```

    Enter a ferry name (or press enter to exit):  Coastal celebration


    Retrieving https://bcferriesapi.ca/v2/capacity
    Retrieved 21736 characters
    Route Code: LNGHSB | From: LNG | To: HSB
      Sailing Time: 6:20 am | Vessel: Queen of Surrey | Fill: 30% | Car Fill: 17% | Status: future
      Sailing Time: 8:40 am | Vessel: Queen of Surrey | Fill: 49% | Car Fill: 53% | Status: future
      Sailing Time: 10:50 am | Vessel: Queen of Surrey | Fill: 40% | Car Fill: 48% | Status: future
      Sailing Time: 1:05 pm | Vessel: Queen of Surrey | Fill: 41% | Car Fill: 27% | Status: future
      Sailing Time: 3:15 pm | Vessel: Queen of Surrey | Fill: 30% | Car Fill: 20% | Status: future
      Sailing Time: 5:25 pm | Vessel: Queen of Surrey | Fill: 25% | Car Fill: 18% | Status: future
      Sailing Time: 6:40 pm | Vessel: Queen of Cowichan | Fill: 7% | Car Fill: 6% | Status: future
      Sailing Time: 8:55 pm | Vessel: Queen of Cowichan | Fill: 12% | Car Fill: 10% | Status: future
      Sailing Time: 6:20 am | Vessel: Queen of Surrey | Fill: 24% | Car Fill: 17% | Status: future
      Sailing Time: 8:40 am | Vessel: Queen of Surrey | Fill: 45% | Car Fill: 48% | Status: future
      Sailing Time: 10:50 am | Vessel: Queen of Surrey | Fill: 35% | Car Fill: 22% | Status: future
    --------------------
    Route Code: NANHSB | From: NAN | To: HSB
      Sailing Time: 6:15 am | Vessel: Queen of Cowichan | Fill: 33% | Car Fill: 29% | Status: future
      Sailing Time: 8:25 am | Vessel: Queen of Oak Bay | Fill: 47% | Car Fill: 55% | Status: future
      Sailing Time: 10:40 am | Vessel: Queen of Cowichan | Fill: 41% | Car Fill: 49% | Status: future
      Sailing Time: 1:00 pm | Vessel: Queen of Oak Bay | Fill: 50% | Car Fill: 51% | Status: future
      Sailing Time: 3:20 pm | Vessel: Queen of Cowichan | Fill: 49% | Car Fill: 46% | Status: future
      Sailing Time: 5:55 pm | Vessel: Queen of Oak Bay | Fill: 54% | Car Fill: 56% | Status: future
      Sailing Time: 8:45 pm | Vessel: Queen of Surrey | Fill: 22% | Car Fill: 25% | Status: future
      Sailing Time: 6:15 am | Vessel: Queen of Cowichan | Fill: 29% | Car Fill: 23% | Status: future
      Sailing Time: 8:25 am | Vessel: Queen of Oak Bay | Fill: 46% | Car Fill: 55% | Status: future
      Sailing Time: 10:40 am | Vessel: Queen of Cowichan | Fill: 47% | Car Fill: 47% | Status: future
    --------------------
    Route Code: SWBTSA | From: SWB | To: TSA
      Sailing Time: 7:00 am | Vessel: Spirit of Vancouver Island | Fill: 90% | Car Fill: 100% | Status: future
      Sailing Time: 9:00 am | Vessel: Spirit of British Columbia | Fill: 81% | Car Fill: 97% | Status: future
      Sailing Time: 11:00 am | Vessel: Spirit of Vancouver Island | Fill: 58% | Car Fill: 65% | Status: future
      Sailing Time: 1:00 pm | Vessel: Spirit of British Columbia | Fill: 77% | Car Fill: 85% | Status: future
      Sailing Time: 3:00 pm | Vessel: Spirit of Vancouver Island | Fill: 75% | Car Fill: 70% | Status: future
      Sailing Time: 5:00 pm | Vessel: Spirit of British Columbia | Fill: 85% | Car Fill: 88% | Status: future
      Sailing Time: 7:00 pm | Vessel: Spirit of Vancouver Island | Fill: 83% | Car Fill: 84% | Status: future
      Sailing Time: 9:00 pm | Vessel: Spirit of British Columbia | Fill: 57% | Car Fill: 46% | Status: future
      Sailing Time: 7:00 am | Vessel: Spirit of Vancouver Island | Fill: 73% | Car Fill: 74% | Status: future
      Sailing Time: 9:00 am | Vessel: Spirit of British Columbia | Fill: 59% | Car Fill: 77% | Status: future
      Sailing Time: 11:00 am | Vessel: Spirit of Vancouver Island | Fill: 69% | Car Fill: 58% | Status: future
    --------------------
    Route Code: HSBNAN | From: HSB | To: NAN
      Sailing Time: 6:15 am | Vessel: Queen of Oak Bay | Fill: 37% | Car Fill: 25% | Status: future
      Sailing Time: 8:25 am | Vessel: Queen of Cowichan | Fill: 35% | Car Fill: 36% | Status: future
      Sailing Time: 10:40 am | Vessel: Queen of Oak Bay | Fill: 36% | Car Fill: 43% | Status: future
      Sailing Time: 1:00 pm | Vessel: Queen of Cowichan | Fill: 40% | Car Fill: 43% | Status: future
      Sailing Time: 3:45 pm | Vessel: Queen of Oak Bay | Fill: 59% | Car Fill: 59% | Status: future
      Sailing Time: 6:35 pm | Vessel: Queen of Surrey | Fill: 55% | Car Fill: 55% | Status: future
      Sailing Time: 10:10 pm | Vessel: Queen of Cowichan | Fill: 13% | Car Fill: 12% | Status: future
      Sailing Time: 6:15 am | Vessel: Queen of Oak Bay | Fill: 33% | Car Fill: 16% | Status: future
      Sailing Time: 8:25 am | Vessel: Queen of Cowichan | Fill: 38% | Car Fill: 40% | Status: future
      Sailing Time: 10:40 am | Vessel: Queen of Oak Bay | Fill: 54% | Car Fill: 60% | Status: future
    --------------------
    Route Code: TSASWB | From: TSA | To: SWB
      Sailing Time: 7:00 am | Vessel: Spirit of British Columbia | Fill: 100% | Car Fill: 100% | Status: future
      Sailing Time: 9:00 am | Vessel: Spirit of Vancouver Island | Fill: 79% | Car Fill: 81% | Status: future
      Sailing Time: 11:00 am | Vessel: Spirit of British Columbia | Fill: 70% | Car Fill: 73% | Status: future
      Sailing Time: 1:00 pm | Vessel: Spirit of Vancouver Island | Fill: 70% | Car Fill: 68% | Status: future
      Sailing Time: 3:00 pm | Vessel: Spirit of British Columbia | Fill: 73% | Car Fill: 68% | Status: future
      Sailing Time: 5:00 pm | Vessel: Spirit of Vancouver Island | Fill: 80% | Car Fill: 80% | Status: future
      Sailing Time: 7:00 pm | Vessel: Spirit of British Columbia | Fill: 72% | Car Fill: 73% | Status: future
      Sailing Time: 9:00 pm | Vessel: Spirit of Vancouver Island | Fill: 64% | Car Fill: 54% | Status: future
      Sailing Time: 7:00 am | Vessel: Spirit of British Columbia | Fill: 70% | Car Fill: 53% | Status: future
      Sailing Time: 9:00 am | Vessel: Spirit of Vancouver Island | Fill: 69% | Car Fill: 56% | Status: future
      Sailing Time: 11:00 am | Vessel: Spirit of British Columbia | Fill: 55% | Car Fill: 62% | Status: future
    --------------------
    Route Code: SWBSGI | From: SWB | To: SGI
      Sailing Time: 5:00 am | Vessel: Salish Heron | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 5:05 am | Vessel: Salish Raven | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 8:15 am | Vessel: Salish Raven | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 9:10 am | Vessel: Salish Heron | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 10:10 am | Vessel: Salish Raven | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 2:20 pm | Vessel: Salish Raven | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 3:15 pm | Vessel: Salish Heron | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 4:30 pm | Vessel: Salish Raven | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 7:10 pm | Vessel: Salish Raven | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 8:00 pm | Vessel: Salish Heron | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 5:00 am | Vessel: Salish Heron | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 5:05 am | Vessel: Salish Raven | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 8:15 am | Vessel: Salish Raven | Fill: 0% | Car Fill: 0% | Status: future
    --------------------
    Route Code: HSBLNG | From: HSB | To: LNG
      Sailing Time: 7:30 am | Vessel: Queen of Surrey | Fill: 43% | Car Fill: 30% | Status: future
      Sailing Time: 9:45 am | Vessel: Queen of Surrey | Fill: 37% | Car Fill: 27% | Status: future
      Sailing Time: 11:55 am | Vessel: Queen of Surrey | Fill: 31% | Car Fill: 22% | Status: future
      Sailing Time: 2:10 pm | Vessel: Queen of Surrey | Fill: 34% | Car Fill: 23% | Status: future
      Sailing Time: 4:20 pm | Vessel: Queen of Surrey | Fill: 36% | Car Fill: 35% | Status: future
      Sailing Time: 5:30 pm | Vessel: Queen of Cowichan | Fill: 16% | Car Fill: 18% | Status: future
      Sailing Time: 7:50 pm | Vessel: Queen of Cowichan | Fill: 20% | Car Fill: 13% | Status: future
      Sailing Time: 10:55 pm | Vessel: Queen of Surrey | Fill: 6% | Car Fill: 3% | Status: future
      Sailing Time: 7:30 am | Vessel: Queen of Surrey | Fill: 37% | Car Fill: 21% | Status: future
      Sailing Time: 9:45 am | Vessel: Queen of Surrey | Fill: 38% | Car Fill: 22% | Status: future
      Sailing Time: 11:55 am | Vessel: Queen of Surrey | Fill: 38% | Car Fill: 24% | Status: future
    --------------------
    Route Code: TSASGI | From: TSA | To: SGI
      Sailing Time: 9:55 am | Vessel: Salish Eagle | Fill: 67% | Car Fill: 100% | Status: future
      Sailing Time: 7:30 pm | Vessel: Salish Eagle | Fill: 71% | Car Fill: 100% | Status: future
      Sailing Time: 9:55 am | Vessel: Salish Eagle | Fill: 86% | Car Fill: 100% | Status: future
      Sailing Time: 7:30 pm | Vessel: Salish Eagle | Fill: 96% | Car Fill: 100% | Status: future
      Sailing Time: 9:55 am | Vessel: (Oct 25, 2024) Salish Eagle | Fill: 100% | Car Fill: 100% | Status: future
    --------------------
    Route Code: TSADUK | From: TSA | To: DUK
      Sailing Time: 5:15 am | Vessel: Queen of Alberni | Fill: 59% | Car Fill: 18% | Status: future
      Sailing Time: 7:45 am | Vessel: Coastal Inspiration | Fill: 63% | Car Fill: 39% | Status: future
      Sailing Time: 10:15 am | Vessel: Queen of Alberni | Fill: 67% | Car Fill: 47% | Status: future
      Sailing Time: 12:45 pm | Vessel: Coastal Inspiration | Fill: 61% | Car Fill: 43% | Status: future
      Sailing Time: 3:15 pm | Vessel: Queen of Alberni | Fill: 75% | Car Fill: 63% | Status: future
      Sailing Time: 5:45 pm | Vessel: Coastal Inspiration | Fill: 64% | Car Fill: 45% | Status: future
      Sailing Time: 8:15 pm | Vessel: Queen of Alberni | Fill: 58% | Car Fill: 30% | Status: future
      Sailing Time: 10:45 pm | Vessel: Coastal Inspiration | Fill: 44% | Car Fill: 6% | Status: future
      Sailing Time: 5:15 am | Vessel: Queen of Alberni | Fill: 54% | Car Fill: 21% | Status: future
      Sailing Time: 7:45 am | Vessel: Coastal Inspiration | Fill: 56% | Car Fill: 27% | Status: future
      Sailing Time: 10:15 am | Vessel: Queen of Alberni | Fill: 55% | Car Fill: 41% | Status: future
    --------------------
    Route Code: SWBFUL | From: SWB | To: FUL
      Sailing Time: 7:00 am | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 9:00 am | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 11:00 am | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 1:00 pm | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 3:00 pm | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 5:00 pm | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 7:00 pm | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 9:00 pm | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 7:00 am | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 9:00 am | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 11:00 am | Vessel: Skeena Queen | Fill: 0% | Car Fill: 0% | Status: future
    --------------------
    Route Code: DUKTSA | From: DUK | To: TSA
      Sailing Time: 5:15 am | Vessel: Coastal Inspiration | Fill: 38% | Car Fill: 24% | Status: future
      Sailing Time: 7:45 am | Vessel: Queen of Alberni | Fill: 61% | Car Fill: 52% | Status: future
      Sailing Time: 10:15 am | Vessel: Coastal Inspiration | Fill: 67% | Car Fill: 54% | Status: future
      Sailing Time: 12:45 pm | Vessel: Queen of Alberni | Fill: 74% | Car Fill: 56% | Status: future
      Sailing Time: 3:15 pm | Vessel: Coastal Inspiration | Fill: 67% | Car Fill: 50% | Status: future
      Sailing Time: 5:45 pm | Vessel: Queen of Alberni | Fill: 73% | Car Fill: 51% | Status: future
      Sailing Time: 8:15 pm | Vessel: Coastal Inspiration | Fill: 54% | Car Fill: 21% | Status: future
      Sailing Time: 10:45 pm | Vessel: Queen of Alberni | Fill: 32% | Car Fill: 11% | Status: future
      Sailing Time: 5:15 am | Vessel: Coastal Inspiration | Fill: 40% | Car Fill: 23% | Status: future
      Sailing Time: 7:45 am | Vessel: Queen of Alberni | Fill: 55% | Car Fill: 42% | Status: future
      Sailing Time: 10:15 am | Vessel: Coastal Inspiration | Fill: 71% | Car Fill: 62% | Status: future
    --------------------
    Route Code: HSBBOW | From: HSB | To: BOW
      Sailing Time: 5:50 am | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 6:50 am | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 8:00 am | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 9:05 am | Vessel: Queen of Cumberland DG Sailing only, No other passengers permitted. Dangerous Goods only | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 10:15 am | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 11:25 am | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 12:35 pm | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 2:20 pm | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 3:30 pm | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 4:35 pm | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 5:45 pm | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 6:50 pm | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 8:00 pm | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 9:00 pm | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 10:00 pm | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 5:50 am | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 6:50 am | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
      Sailing Time: 8:00 am | Vessel: Queen of Cumberland | Fill: 0% | Car Fill: 0% | Status: future
    --------------------



```python

```
