# Quick Note for Colab
Hi everyone!

If you run the colab file, and receive the error: TypeError: 'Box' object is not iterable please use the following solution from: 

https://www.udemy.com/course/artificial-intelligence-az/learn/lecture/22309648#questions/13954732/

Thank you Tadeusz for sharing the details!

If you get an error like this:

```bash
File "/vizdoomgym/vizdoomgym/envs/vizdoomenv.py", line 147, in __collect_observations    
for space in self.observation_space:TypeError: 'Box' object is not iterable
```
Open the file "/vizdoomgym/vizdoomgym/envs/vizdoomenv.py" at line 147 and replace the following line:

```py
for space in self.observation_space: 
    observation.append(np.zeros(space.shape, dtype=space.dtype))
```
with the following: 
```py
if isinstance(self.observation_space, gym.spaces.box.Box):    
# Box isn't iterable    
obs_space = [self.observation_space]else:    
obs_space = self.observation_space  for space in obs_space:    
observation.append(np.zeros(space.shape, dtype=space.dtype))
```
---
Source: https://github.com/shakenes/vizdoomgym/pull/8/files/9ffe3d0f1d470e5fb07d78b476d94fcf3648d570