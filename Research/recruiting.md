### google

- What do you think was the biggest learning curve for you moving from your previous role to Big Tech? 
- How much room is there for bottom-up initiative versus roadmap-driven work on this team?


## sutter hill ventures

1. What are SHV's current focus areas? What are you guys particularly excited about right now?
2. How does team matching work?
3. To what extent does SHV impact the direction that these companies go in?
4. How do you ensure that your portfolio companies can compete in such a saturated AI space?

What I'm looking for in a company:
- at the very least reached product-market fit
	- More ideally a more mature startup
- I care most about the team -- being able to learn at my first FT job out of school


### nuro
- **Onboard Systems:** Our onboard system team’s software engineers provide a reliable and high-performance platform that allows our autonomy teams to integrate their autonomy software and algorithms that work across various self-driving platforms. 

- **Technical Infrastructure:** this group owns few fundamental services for entire engineering organizations: generic compute platform to host mission-critical workflows such as data processing and simulation, storage management service which manages hundreds of PB of data, cloud infrastructure serves as IaaC which provisions and maintains all cloud resources, engineering productivity provides tools such as build and CI/CD to make engineering work more efficient.

ML Data Infrastructure org
mini-onsite (virtual)
- coding - algorithms
- coding - systems
	- memory, multithreading, concurrency
- hiring manager
	- resume deep dive

final chat w/ VP AI Platform
- high level, motivation, culture fit
- could have some questions about technical experience

Questions
- I saw on the website that you guys  have ambitions to skill Nuro Driver to all types of vehicles. I saw things like going from the delivery stuff (I guess that was your old path) up to even trucks. I'm wondering what the focus of the company is right now: whether you're all hands-on with this tangible partnership that you already have on the books or if you're actively trying to scale into those broader avenues as well. Where effort is being concentrated right now?
- What would you say are the biggest constraints that you guys have right now or challenges that you are facing?
-  What's made you really buy into Nuro as a company and want to stay for the long term?

Values
-  ownership, hard work, and initiative
- continuous improvement and learning from those around me 


pre-offer call
- tentative start date 6/22 (can be pushed back, even after signing)
- rsu
- email about office meet
- new hire equity is non-negotiable after signing

## latch bio
- OpenEvidence: Jan 2026 closed Series D $250M raise (led by Sequoia) at 12B valuation 
- Abridge: June 2025 closed Series E $300M raise (led by a16z) at 5B valuation
- Ambience Healthcare: July 2025 closed Series C $243M raise (a16z, OpenAI startup fund) at 1.25B valuation
- Cairns Health: Khosla Ventures backed, more lowkey but founded in 2017
	- digital health for seniors, Luna (smart home voice activated, app controlled device)
- Ellipsis Health: KV backed, $45M Series A in June 2025, AI care manager Sage

Who are Latch's customers? Therapeutics and pharmaceuticals companies?
Latch: 28M series A in 2022 --> don't need more money
- What do you think about these startups that raise big flashy rounds every year? When do you think that makes sense?

New grad opportunities at these places are very rare, barrier to entry gets higher and higher. I want to get into industry now

---

# behavioral

**S**ituation: Describe the situation you were in or the task you needed to accomplish  
**T**ask: Explain the goal you were working toward  
**A**ctivity: Detail the specific steps you took and the role(s) you played  
**R**esult: Describe your accomplishments and the overall outcome

Areas to highlight:
- Communication
- Time Management
- Flexibility
- Leadership
- Initiative
- Problem Solving
- Organization
- Decision Making

Hypotheticals:
1. An understanding of the problem: Did you display a general understanding of the question asked by outlining what experiences and factors are relevant to solve the problem and what additional work needs to be done?
2. Thoughtful problem solving: Are you gathering information in order to address specific factors or pulling from specific experience? Are you thinking about how to gather information or conduct research and how to use that information to solve the problem? Are you getting to the root cause?
3. Potential solutions: Does your solution answer the initial question or solve the initial problem? Are you considering and appropriately weighing the pros and cons of your solution?
4. Support for your solutions: Are you providing rationale for why a certain solution is best, despite previously stated pros and cons? Did you describe potential success metrics to support your solution?
5. Strong communication: Are your responses structured and logical? Do you balance brevity and detail?

---
# python programming

## built-ins

- **lst.sort()** (in place), **sorted(lst)** (copy)
	- N log N time complexity
	- key = sort function, reverse = True if descending (ascending default)

`import bisect`
Given a sorted list:
Bisect O(log n)
- `bisect_left(sorted_list, new_item, key=Optional_fn) --> leftmost insertion index`
- `bisect_right(sorted_list, new_item) --> rightmost insertion index`
Insort = Insert O(n) + Search O(log n) = O(n)
- `insort(sorted_list, new_item, key=Optional_search_fn) --> None` , inserts new_item into sorted_list in place
	- Does insort_right, insort_left also exists

## data structures

`from collections import ...`
- **deque** (double ended queue)
	- append, pop, appendleft, popleft
	- `rotate(n)`: rotates n elements right (or left if negative)
	- `deque(maxlen=Optional_int)`: once maxlen reached, evict from other side

`import heapq`
- **heapq** (heap queue)
	- heapq.heapify(lst): list to min-heap (or heapify_max(lst))
	- heapq.heappush(heap, item)
	- heapq.heappop(heap): if heap is empty, [`IndexError`](https://docs.python.org/3/library/exceptions.html#IndexError "IndexError") is raised. To access the smallest item without popping it, use `heap[0]`.

General purpose functions (not heapq, but use heap for efficiency)
	- heapq.merge(lst, lst2, ..., key=None, reverse=False) --> iterable: merge n sorted lists 
		- If reverse=True, lsts must also be sorted in descending order
	- nlargest(n, iterable, key=None): or nsmallest

[[systems & networking prep]]