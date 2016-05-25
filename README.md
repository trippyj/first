# firstecho "# first" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/trippyj/first.git
git push -u origin master
001.
/* @pjs preload="color.jpg"; */
 
HPixelColorist colors;
HRect  r1;
HTween tween;
HCallback tr, br, bl, tl;
int marginOffset = 150;
float tweenEase = 0.01;
float tweenSpeed = 0.9;
 
void setup() {
size(640,640);
H.init(this).background(#202020).autoClear(false);
smooth();
 
colors = new HPixelColorist("color.jpg").fillOnly();
 
r1 = new HRect(100).rounding(10);
r1
.stroke(#000000, 100)
.fill(#FF3300)
.anchor(50,-50)
// .anchorAt(H.CENTER)
.loc(marginOffset,marginOffset)
.rotation(45)
;
H.add(r1);
 
new HOscillator()
.target(r1)
.property(H.ROTATION)
.range(-180, 180)
.speed(1)
.freq(2)
;
 
new HOscillator()
.target(r1)
.property(H.SCALE)
.range(0.2, 1)
.speed(0.5)
.freq(15)
;
 
// tween from center to TL corner
 
tween = new HTween()
.target(r1).property(H.LOCATION)
.start(r1.x(), r1.y())
.end(marginOffset, marginOffset)
051.
.ease(1).spring(0)
052.
;
053.
 
054.
// tween from TL to TR corner
055.
 
056.
tr = new HCallback() {
057.
public void run(Object obj) {
058.
tween.start( r1.x(), r1.y() ).end( width-marginOffset, marginOffset )
059.
.ease(tweenEase).spring(tweenSpeed)
060.
.register().callback(br);
061.
}
062.
};
063.
 
064.
// tween from TR to BR corner
065.
 
066.
br = new HCallback() {
067.
public void run(Object obj) {
068.
tween.start( r1.x(), r1.y() ).end( width-marginOffset, height-marginOffset )
069.
.ease(tweenEase).spring(tweenSpeed)
070.
.register().callback(bl);
071.
}
072.
};
073.
 
074.
// tween from BR to BL corner
075.
 
076.
bl = new HCallback() {
077.
public void run(Object obj) {
078.
tween.start( r1.x(), r1.y() ).end( marginOffset, height-marginOffset )
079.
.ease(tweenEase).spring(tweenSpeed)
080.
.register().callback(tl);
081.
}
082.
};
083.
 
084.
// tween from BL to TL corner
 
tl = new HCallback() {
public void run(Object obj) {
tween.start( r1.x(), r1.y() ).end( marginOffset, marginOffset )
.ease(tweenEase).spring(tweenSpeed)
.register().callback(tr);
}
};
 
094.
tween.register().callback(tr);
095.
}
096.
 
097.
void draw() {
098.
colors.applyColor(r1);
099.
H.drawStage();
100.
}
101.
 
