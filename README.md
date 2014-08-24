blast
=====
 BOOL numTrack = NO;
30	30	 BOOL arrTrack = NO;
31	31	 
32	+BOOL readyToExit = NO;
33	+
32	34	 - (void)viewDidLoad
33	35	 {
34	36	     [super viewDidLoad];
35	37	 
36	38	     unsigned char bytes[] = {0xde,0xad,0xbe,0xef};
37	39	     data = [NSData dataWithBytes:bytes length:sizeof(bytes)];
38		-    num = [[NSNumber alloc] initWithInt:0xefbeadde];
40	+    num = [[NSNumber alloc] initWithInt:0xbebafeca];
39	41	     str = [[NSString alloc] initWithFormat:@"0123456789ABCDEF"];
40	42	     
41	43	     arr = [[NSArray alloc] initWithObjects:data,num,str,nil];
...	...	@@ -86,11 +88,11 @@ - (IBAction)StrUnlock:(id)sender {
86	88	 - (IBAction)StringTrack:(id)sender {
87	89	     if(strTrack == YES) {
88	90	         untrack(str);
89		-        [self.StrTrackButton setTitle:@"Track" forState:UIControlStateNormal];
91	+        [self.StrTrackButton setTitle:@"track" forState:UIControlStateNormal];
90	92	         strTrack = NO;
91	93	     } else {
92	94	         track(str);
93		-        [self.StrTrackButton setTitle:@"Untrack" forState:UIControlStateNormal];
95	+        [self.StrTrackButton setTitle:@"untrack" forState:UIControlStateNormal];
94	96	         strTrack = YES;
95	97	     }
96	98	 }
...	...	@@ -113,11 +115,11 @@ - (IBAction)DataUnlock:(id)sender {
113	115	 - (IBAction)DataTrack:(id)sender {
114	116	     if(dataTrack == YES) {
115	117	         untrack(data);
116		-        [self.DataTrackButton setTitle:@"Track" forState:UIControlStateNormal];
118	+        [self.DataTrackButton setTitle:@"track" forState:UIControlStateNormal];
117	119	         dataTrack = NO;
118	120	     } else {
119	121	         track(data);
120		-        [self.DataTrackButton setTitle:@"Untrack" forState:UIControlStateNormal];
122	+        [self.DataTrackButton setTitle:@"untrack" forState:UIControlStateNormal];
121	123	         dataTrack = YES;
122	124	     }
123	125	 }
...	...	@@ -140,11 +142,11 @@ - (IBAction)NumberUnlock:(id)sender {
140	142	 - (IBAction)NumberTrack:(id)sender {
141	143	     if(numTrack == YES) {
142	144	         untrack(num);
143		-        [self.NumTrackButton setTitle:@"Track" forState:UIControlStateNormal];
145	+        [self.NumTrackButton setTitle:@"track" forState:UIControlStateNormal];
144	146	         numTrack = NO;
145	147	     } else {
146	148	         track(num);
147		-        [self.NumTrackButton setTitle:@"Untrack" forState:UIControlStateNormal];
149	+        [self.NumTrackButton setTitle:@"untrack" forState:UIControlStateNormal];
148	150	         numTrack = YES;
149	151	     }
150	152	 }
...	...	@@ -167,11 +169,11 @@ - (IBAction)ArrayUnlock:(id)sender {
167	169	 - (IBAction)ArrayTrack:(id)sender {
168	170	     if(arrTrack == YES) {
169	171	         untrack(arr);
170		-        [self.ArrTrackButton setTitle:@"Track" forState:UIControlStateNormal];
172	+        [self.ArrTrackButton setTitle:@"track" forState:UIControlStateNormal];
171	173	         arrTrack = NO;
172	174	     } else {
173	175	         track(arr);
174		-        [self.ArrTrackButton setTitle:@"Untrack" forState:UIControlStateNormal];
176	+        [self.ArrTrackButton setTitle:@"untrack" forState:UIControlStateNormal];
175	177	         arrTrack = YES;
176	178	     }
177	179	 }
...	...	@@ -182,13 +184,13 @@ - (IBAction)WipeAll:(id)sender {
182	184	 }
183	185	 
184	186	 - (IBAction)LockAll:(id)sender {
185		-    lockAll(@"TEST");
187	+    lockAll(@"PASS");
186	188	     [self updateWidgets];
187	189	     
188	190	 }
189	191	 
190	192	 - (IBAction)UnlockAll:(id)sender {
191		-    unlockAll(@"TEST");
193	+    unlockAll(@"PASS");
192	194	     [self updateWidgets];
193	195	 }
194	196	 
...	...	@@ -207,4 +209,15 @@ - (IBAction)ChecksumAll:(id)sender {
207	209	     }
208	210	     [alert show];
209	211	 }
212	+
213	+- (IBAction)SecureExit:(id)sender {
214	+    if (readyToExit)
215	+        exit(0);
+    else {
217	+        secureExit();
218	+        [self.ExitButton setTitle:@"exit"];
219	+        [self updateWidgets];
220	+        readyToExit = YES;
221	+    }
	222	+}
