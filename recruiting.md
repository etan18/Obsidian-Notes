
### amd
- As a primarily hardware company, what are AMD's current plans on the software AI/ML side of things?
	- Does the company view ML development as primarily being for internal tooling or does it have plans to go to market?
- Program
	- What are the expectations? 
	- Are interns working on standalone projects, or will they integrate more into day-to-day work on AI/ML teams?
- What are you most excited about at AMD right now?

Why AMD?
- I think the way you guys are positioned now especially in this AI boom that's centered in the Bay Area is really exciting
- So much opportunity for growth in this area
- I want to build tools and products that are impactful to end users
- Being from primarily academia, one of the most frustrating things is compute constraints and not really being able to scale to the level that is being demanded -- an issue that AMD certainly doesn't face given its product line

Introduce yourself
- I am currently doing research on AI for healthcare, making sure that the tools we integrate into real-world clinics are actually improving clinician load and patient care
- One particular problem with deploying predictive clinical decision models is the differences between different hospitals (protocols, levels of care, etc.)
	- I previously focused on data scaling solutions for correcting distribution shift in predictive models
	- Right now, I'm looking more at the algorithmic side of things --- distributionally-aware prediction


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