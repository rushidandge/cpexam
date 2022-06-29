import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStreamReader;
import java.util.Arrays;
import java.util.StringTokenizer;

class Main {
	
	public static boolean [][] mat;
	public static int [] color;
	
	public static boolean fillColor (int id, int toFill) {
		if (color[id]==Integer.MAX_VALUE) {
			boolean flag=true;
			color[id]=toFill;
			for (int i=0;i<mat.length && flag;i++) {
				if (mat[id][i]) {
					flag=fillColor(i,1-toFill);
				}
			}
			return flag;
		} else if (color[id]!=toFill) {
			return false;
		}
		return true;
	}
	
	public static void main(String[] args) throws IOException {
		BufferedReader br=new BufferedReader(new InputStreamReader(System.in));
		while (true) {
			int n=Integer.parseInt(br.readLine());
			if (n==0) {
				break;
			}
			int l=Integer.parseInt(br.readLine());
			mat=new boolean [n][n];
			color=new int [n];
			Arrays.fill(color, Integer.MAX_VALUE);
			
			for (int i=0;i<l;i++) {
				StringTokenizer st=new StringTokenizer(br.readLine());
				int src=Integer.parseInt(st.nextToken());
				int dest=Integer.parseInt(st.nextToken());
				if (src!=dest) {
					mat[src][dest]=true;
					mat[dest][src]=true;
				}
			}
			
			if (fillColor(0,0)) {
				System.out.println("BICOLORABLE.");
			} else {
				System.out.println("NOT BICOLORABLE.");
			}
		}
	}
}
