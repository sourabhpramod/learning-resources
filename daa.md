# Computational Geometry:


Point in Rectangle
Assume that rectangle is represented by the 4 points P,Q,R,S in two dimensional plane in counter clockwise direction . Let   T be any point on the two dimensional plane. Design an algorithm to check whether the given point T is inside, outside  and on any line segment of the given rectangle.  Implement your algorithm in any programming language. Print 1 if T is inside of the rectangle , print -1 If it is outside of the rectangle and Print 0 if T is on any line segement of the rectangle.

Input format

Enter 4 points for rectangle

 Enter point T

Output

Print 1 if T is inside of the rectangle.

Print -1 if T is outside of the rectangle.

Print 0 if T is on  any one line segment of the rectangle.

## Answer:

```c++
#include <iostream>

using namespace std;

int cp(pair<double, double> p, pair<double, double> q, pair<double, double> r) {
    double val = (r.second - p.second) * (q.first - p.first) - (q.second - p.second) * (r.first - p.first);
    if (val == 0) return 0;  
    else if (val > 0) return 1;  
    else return 2;  
}

bool onSegment(pair<double, double> p, pair<double, double> q, pair<double, double> r) {
    return (min(p.first, r.first) <= q.first && q.first <= max(p.first, r.first) && min(p.second, r.second) <= q.second && q.second <= max(p.second, r.second));
}

int check(pair<double,double> P, pair<double,double> Q, pair<double,double> R, pair<double,double> S, pair<double,double> T){
    int o1 = cp(P,Q,T);
    int o2 = cp(Q,R,T);
    int o3 = cp(R,S,T);
    int o4 = cp(S,P,T);
   
    if(o1==o2 && o2==o3 && o3==o4 && o4==o1){
        return 1;
    }
    
    if ((o1 == 0 && onSegment(P, T, Q)) || (o2 == 0 && onSegment(Q, T, R)) || (o3 == 0 && onSegment(R, T, S)) || (o4 == 0 && onSegment(S, T, P))) {
        return 0;  
    }

    return -1;
    
}

int main(){
    pair<double, double> P,Q,R,S,T;
    cin >> P.first >> P.second;
    cin >> Q.first >> Q.second;
    cin >> R.first >> R.second;
    cin >> S.first >> S.second;
    cin >> T.first >> T.second;
    
    
    int result = check(P,Q,R,S,T);
    cout<<result;
}

```

---

Perpendicular Line Segments
Let S be a set of n line segments in two dimensional planes. Design an algorithm to count the number of pairs of line segments which are perpendicular. Your algorithm should not use the division operation and trigonometric functions. Cartesian coordinates of the end points of the line segment are given. For example,  n= 3 line segments are 

0  0      0 2

0 0      1 0

 0 0     1 1

 The ouput of your program  should be1

Input Format:

Enter the number of lines.

Enter the end points of each line 

Output Format:

Number of line segments which are perpendicular.

## Answer:

```c++
#include <iostream>
#include <vector>
using namespace std;

struct Line {
    int x1, y1, x2, y2;
};

int main() {
    int n, count = 0;
    cin >> n;
    vector<Line> lines(n);
    for (int i = 0; i < n; i++) {
        cin >> lines[i].x1 >> lines[i].y1 >> lines[i].x2 >> lines[i].y2;
    }
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            int dx1 = lines[i].x2 - lines[i].x1;
            int dy1 = lines[i].y2 - lines[i].y1;
            int dx2 = lines[j].x2 - lines[j].x1;
            int dy2 = lines[j].y2 - lines[j].y1;
            if (dx1 * dx2 + dy1 * dy2 == 0) {
                count++;
            }
        }
    }
    cout << count << endl;
    return 0;
}
```

## Graham's Scan:

```c++
#include <iostream>
   #include <vector>
   #include <algorithm>
   #include <stack>
   #include <cmath>
   
   using namespace std;
   
   struct Point {
       int x, y;
   };
   
   // Function to find the polar angle
   double polarAngle(const Point& p0, const Point& p) {
        return atan2(p.y - p0.y, p.x - p0.x);
   }
   
   // Function to calculate the cross product
   int crossProduct(const Point& a, const Point& b, const Point& c) {
        return (b.x - a.x) * (c.y - a.y) - (b.y - a.y) * (c.x - a.x);
   }
   
   // Function to compute the convex hull using Graham Scan
   vector<Point> grahamScan(vector<Point>& points) {
        // Find the point with the minimum y-coordinate
        int minY = 0;
        for (int i = 1; i < points.size(); ++i) {
            if (points[i].y < points[minY].y || (points[i].y == points[minY].y && points[i].x < points[minY].x)) {
                minY = i;
            }
        }
        swap(points[0], points[minY]); // Swap the lowest point to the beginning
    
        // Sort points by polar angle with respect to the lowest point
        sort(points.begin() + 1, points.end(), [&](const Point& a, const Point& b) {
            double angleA = polarAngle(points[0], a);
            double angleB = polarAngle(points[0], b);
            if (angleA == angleB) {
                return (pow(points[0].x - a.x, 2) + pow(points[0].y - a.y, 2)) < (pow(points[0].x - b.x, 2) + pow(points[0].y - b.y, 2)); //Distance if angles are same
            }
            return angleA < angleB;
        });
    
        // Build the convex hull
        stack<Point> hull;
        hull.push(points[0]);
        hull.push(points[1]);
        hull.push(points[2]);
    
        for (int i = 3; i < points.size(); ++i) {
            Point top = hull.top();
            hull.pop();
            while (crossProduct(hull.top(), top, points[i]) <= 0) { // Non-left turn
                top = hull.top();
                hull.pop();
            }
            hull.push(top);
            hull.push(points[i]);
        }
    
        // Copy the hull points from the stack to a vector
        vector<Point> result;
        while (!hull.empty()) {
            result.push_back(hull.top());
            hull.pop();
        }
        return result;
   }
   
   int main() {
        vector<Point> points = {{0, 3}, {1, 1}, {2, 2}, {4, 4}, {0, 0}, {1, 2}, {3, 1}, {3, 3}};
        vector<Point> convexHullPoints = grahamScan(points);
    
        cout << "Convex Hull Points:\n";
        for (const auto& p : convexHullPoints) {
            cout << "(" << p.x << ", " << p.y << ")\n";
        }
    
        return 0;
   }
```
## Jarvis March:

```c++

#include <iostream>
   #include <vector>
   #include <algorithm>
   #include <cmath>
   
   using namespace std;
   
   struct Point {
       int x, y;
   };
   
   // Function to calculate the cross product
   int crossProduct(const Point& a, const Point& b, const Point& c) {
        return (b.x - a.x) * (c.y - a.y) - (b.y - a.y) * (c.x - a.x);
   }
   
   // Function to compute the convex hull using Jarvis's March
   vector<Point> jarvisMarch(vector<Point>& points) {
        if (points.empty()) return {};
    
        vector<Point> hull;
    
        // Find the leftmost point
        int leftMost = 0;
        for (int i = 1; i < points.size(); ++i) {
            if (points[i].x < points[leftMost].x) {
                leftMost = i;
            }
        }
    
        int p = leftMost, q;
        do {
            hull.push_back(points[p]);
            q = (p + 1) % points.size(); 
            for (int i = 0; i < points.size(); ++i) {
                if (crossProduct(points[p], points[i], points[q]) > 0) {
                    q = i;
                }
            }
            p = q;
        } while (p != leftMost);
    
        return hull;
   }
   
   int main() {
        vector<Point> points = {{0, 3}, {1, 1}, {2, 2}, {4, 4}, {0, 0}, {1, 2}, {3, 1}, {3, 3}};
        vector<Point> convexHullPoints = jarvisMarch(points);
    
        cout << "Convex Hull Points:\n";
        for (const auto& p : convexHullPoints) {
            cout << "(" << p.x << ", " << p.y << ")\n";
        }
    
        return 0;
   }
```
