# [350.Intersection of Two Arrays II](https://leetcode-cn.com/problems/intersection-of-two-arrays-ii/)
# 思路1（速度最快）
把长度较大的数组存于 map 中，这个 map 记录各个元素的数量。
对长度较小的数组中的每个元素，在 map 中查找。若找到并且值不为0，则存入交集中，并且值减1。

```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        vector<int> interset;
        if(!nums1.size() || !nums2.size())
            return interset;
        map<int, int> m;
        if(nums1.size()<nums2.size())
            swap(nums1, nums2);     // 把大的放在数组放在 map 里，小的数组查找
        for(int i=0;i<nums1.size();i++){
            if(!m.count(nums1[i]))
                m.insert(map<int,int>::value_type(nums1[i],1));
            else
                m[nums1[i]]++;
        }
        for(int i=0;i<nums2.size();i++){
            if(m.count(nums2[i])){
                if(m[nums2[i]]!=0){
                    m[nums2[i]]--;
                    interset.push_back(nums2[i]);
                }
            }
        }
        return interset;
    }
};
```

# 思路2
在遍历第一个数组，每个元素都在第二个数组中找到相同的元素，若存在，则删掉第二个数组对应的元素，并把该元素存到交集中。

```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        vector<int> interset;
        int len1 = nums1.size(), len2 = nums2.size();
        if(len1==0 || len2==0)
            return interset;
        for(int i=0;i<len1;i++){
            vector<int>::iterator it = find(nums2.begin(), nums2.end(), nums1[i]);
            if(it!=nums2.end()){
                interset.push_back(*it);
                nums2.erase(it);
                if(nums2.empty())
                    break;
            }
        }
        return interset;
    }
};
```

# 思路3(速度比2快)
先对俩数组排序,一旦找到相同的元素，下一次查找位置不需要从头开始，直接从下一个位置查找

```c++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        vector<int> interset;
        int len1=nums1.size(), len2=nums2.size();
        int i=0,j=0;
        if(len1==0 || len2==0)
            return interset;
        sort(nums1.begin(), nums1.end());
        sort(nums2.begin(), nums2.end());
        while(i<len1 && j<len2){
            if(nums1[i]==nums2[j]){
                interset.push_back(nums1[i]);
                i++;j++;
            }
            else if(nums1[i]<nums2[j])
                i++;
            else
                j++;
        }        
        return interset;
    }
};
```