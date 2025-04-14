# YouTube Channel Analytics Tool

A Python-based tool to analyze YouTube channel statistics using the YouTube Data API v3.

## Project Overview
This project fetches and analyzes statistics from multiple YouTube channels including subscriber count, view counts, and video counts.

## Requirements
- Python 3.x
- Google API Client Library for Python
```bash
pip install -r reqs.txt

## Setup
Create a virtual environment:
```bash
python -m venv env
source env/bin/activate  # On Unix/macOS
.\env\Scripts\activate  # On Windows
```
Configure your YouTube API key in .env file

## Code Explanation
Main Function: get_channel_states

```python
from googleapiclient.discovery import build

youtube = build('youtube', 'v3', developerKey=api_key)

def get_channel_states(youtube, channel_ids):
    all_data = []  # Initialize empty list to store channel data
    
    # Create API request to fetch channel details
    request = youtube.channels().list(
        part='snippet,contentDetails,statistics',  # Request specific parts of channel data
        id=','.join(channel_ids)  # Join multiple channel IDs with commas
    )
    
    # Execute the API request
    response = request.execute()
    
    # Process each channel's data
    for i in range(len(response['items'])):
        # Extract and structure channel information
        data = dict(
            channel_name=response['items'][i]['snippet']['title'],  # Get channel name
            Subscibers=response['items'][i]['statistics']['subscriberCount'],  # Get subscriber count
            views=response['items'][i]['statistics']['viewCount'],  # Get total view count
            total_videos=response['items'][i]['statistics']['videoCount']  # Get total videos count
        )
        all_data.append(data)  # Add channel data to results list
    
    return all_data
```

## Sample Channels Analyzed
The project currently analyzes several music artist channels including:

J. Cole
Joyner Lucas
Eminem
And more

## Example Output
The tool returns a list of dictionaries containing channel statistics:
```python
[
    {
        'channel_name': 'J. Cole - Topic',
        'Subscibers': '102000',
        'views': '1971004045',
        'total_videos': '361'
    },
    # ... more channels
]
```

