# 2024 Paris Olympics Video Danmaku Analysis and Mining

This project focuses on analyzing and mining danmaku (bullet comments) from videos related to the 2024 Paris Olympics. By scraping data from Bilibili (B站), it explores public perceptions of AI technology applications during the event, complemented by data visualization and statistical insights into the fusion of technology and sports.

## Project Background

The 33rd Summer Olympic Games (Paris 2024) took place from July 26 to August 11, 2024, in Paris, France. Marking Paris's third time hosting the Summer Olympics (after 1900 and 1924), it became the second city after London to achieve this feat. The United States topped the medal tally with 40 gold medals and 126 total medals, tied with China for gold (40) but ahead in total medals (91 for China). Host nation France secured 16 gold medals and 64 total medals, ranking fifth. The 2024 Paris Olympics was not only a sporting spectacle but also a showcase of industrial digitization, with AI technology seamlessly integrated into event organization, broadcasting, and audience experiences, heralding a new era of tech-enhanced sports.

This project scrapes danmaku from Bilibili to analyze AI technology applications in the 2024 Paris Olympics, uncovering trends in the intersection of technology and athletics.

## Task Requirements

### Data Collection
- Use a web crawler to scrape danmaku from the top 300 videos on Bilibili, ranked by comprehensive sorting, using the keyword "2024 Paris Olympics."

### Data Analysis
- Count the occurrences of danmaku related to AI technology applications and list the top 8 by frequency.
- Automatically export the statistical results to an Excel file.

### Data Visualization
- Create a visually appealing word cloud to represent the collected dataset.

### Data Insights
- Derive mainstream opinions among Bilibili users regarding AI technology use in the 2024 Paris Olympics based on the statistical data.

### Optional Bonus Tasks
- Scrape perspectives from global mainstream media to predict event trends.
- Freestyle: Explore interesting datasets, create a creative data visualization dashboard, or other fun and innovative analyses.

## Use Cases
- Study AI technology applications and public feedback during the 2024 Paris Olympics.
- Learn techniques for data scraping, processing, and visualization.
  
# Project Implementation Details

## Project Planning and Development Process

### Project Phases
1. Requirements Analysis
   - Understanding task requirements
   - Defining project scope and features
   - Planning development approach

2. Technical Research
   - Researching required APIs
   - Evaluating necessary Python libraries
   - Determining optimal implementation methods

3. Implementation
   - Developing core functionality modules
   - Building data collection and processing systems
   - Creating visualization components

4. Testing and Optimization
   - Conducting code testing
   - Resolving bugs and exceptions
   - Implementing performance improvements

5. Results Generation
   - Creating data visualizations
   - Generating Excel reports
   - Producing final analysis results

## Technical Implementation

### Key Technologies Used
1. Data Collection
   - Browser Developer Tools
   - JSON file analysis
   - Python Regular Expressions
   - File I/O operations

2. Data Processing
   - Requests library
   - Regular Expressions (re)
   - OpenPyXL
   - Pandas
   - Collections
   - ThreadPoolExecutor

3. Data Visualization
   - WordCloud
   - Jieba
   - ImageIO
   - Adobe Photoshop

### Performance Optimization

#### Initial Performance Issues
- API request time: 295 seconds
- Network requests: 445 seconds
- Total execution time: 467 seconds

#### Optimization Strategies
1. Reduced API Call Frequency
   ```python
   async def fetch_all_bulletchats(session):
       all_bulletchats = []
       tasks = []
       total_requests = 6 * 50
       for i in range(total_requests):
           page_number = i // 50 + 1
           index = i % 50
           tasks.append(asyncio.ensure_future(
               fetch_bulletchat_data(session, page_number, index)))
       return all_bulletchats
   ```

2. HTTP Connection Reuse
   ```python
   async def fetch_and_save_bulletchat(session, cid):
       url = tempApi.replace("{number}", str(cid))
       try:
           async with session.get(url) as response:
               response_text = await response.text()
               data = re.findall('(.*?)', response_text)
               return data if data else []
       except:
           return []
   ```

3. Asynchronous I/O Implementation
   ```python
   async def get_bvid(session, page, index):
       if (page, index) in bvid_cache:
           return bvid_cache[(page, index)]
       url = f'https://api.bilibili.com/x/web-interface/search/type?...'
       async with session.get(url) as response:
           try:
               json_data = await response.json()
               bvid = json_data['data']['result'][index]['bvid']
               bvid_cache[(page, index)] = bvid
               return bvid
           except Exception as e:
               print(f"Error getting bvid: {e}")
               return None
   ```

4. Caching Implementation
   ```python
   # Global cache for bvid and cid
   bvid_cache = {}
   cid_cache = {}
   ```

#### Optimization Results
- Main program execution time reduced from 467s to 4.07s
- Data processing time: 3.02s
- File operations: ~2.11s
- Network wait time: <1s

## Testing Implementation

### Unit Testing Example
```python
@Test
def testLoginSuccess():
    # Arrange
    loginReq = LoginReq("testuser", "testpass")
    teacher = Teacher()
    teacher.setId(1L)
    teacher.setName("John Doe")
    
    # Act
    result = teacherService.login(loginReq)
    
    # Assert
    assertEquals(200, result.getCode())
```

### Performance Testing
- Used JProfiler for performance analysis
- Implemented HTTP request testing
- Monitored API response times
- Analyzed memory usage patterns

## Data Analysis and Visualization

### Data Processing Components
- Text processing using Jieba
- Image recognition with ImageIO
- Custom stopwords configuration
- WordCloud generation settings

### Visualization Interface
- Time-based data display
- Score distribution charts
- Student performance analytics
- Interactive data filtering
