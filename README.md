# Conway-s-Game-of-Life
import zen.core.Zen;


public class Grid_of_Integers {
	static boolean[][] grid = new boolean [50][50];

	public static void main(String[] args) {
		Zen.create(500,500);
		randomize();

		while (true) {
			Zen.buffer(100);
			draw();
			step();
			
			checkClick();
		}

	}

	private static void checkClick() {
		int lastX = 0;
		int lastY = 0;
		if (Zen.getMouseClickX() != lastX && Zen.getMouseClickY() != lastY) {
			lastX= Zen.getMouseClickX();
			lastY = Zen.getMouseClickY();
		}
		
	}

	public static void step() {
		boolean[][] newGrid = new boolean[50][50];

		for (int x = 0 ; x < 50 ; x++) {
			for (int y = 0 ; y < 50 ; y++) {
				// Get how many neighbors this cell has.
				int count = neighbors(x, y);

				// 1. If the square is alive, but has less than two neighbors, it dies.
				if (grid[x][y] == true && count < 2) {
					newGrid[x][y] = false;
				}
				// 2. If the square is alive and has two or three neighbors, it lives.
				if (grid[x][y] == true && (count == 2 || count == 3)) {
					newGrid[x][y] = true;
				}

				// 3. If the square is alive and has more than three neighbors, it dies.
				if (grid[x][y] == true && count > 3) {
					newGrid[x][y] = false;
				}

				// 4. If a square is dead, and it has exactly three live neighbors, it becomes alive.
				if (grid[x][y] == false && count == 3) {
					newGrid[x][y] = true;
				}
			}
		}

		grid = newGrid;
	}

	public static int neighbors(int x, int y) {
		int count = 0;

		if (x > 0 && y > 0 && grid[x - 1][y - 1] == true) {
			count++;
		}
		if (y > 0 && grid[x][y - 1] == true) {
			count++;
		}
		if (x < 49 && y > 0 && grid[x + 1][y - 1] == true) {
			count++;
		}
		if (x > 0 && grid[x - 1][y] == true) {
			count++;
		}
		if (x < 49 && grid[x + 1][y] == true) {
			count++;
		}
		if (x > 0 && y < 49 && grid[x - 1][y + 1] == true) {
			count++;
		}
		if (y < 49 && grid[x][y + 1] == true) {
			count++;
		}
		if (x < 49 && y < 49 && grid[x + 1][y + 1] == true) {
			count++;
		}


		return count;
	}


//Show the state of the grid

public static void draw() {
	Zen.setBackground("white");
	Zen.setColor("black");
	for (int x = 0; x < 50; x++) {
		for (int y = 0; y < 50; y ++) {
			if (grid[x][y] == true) {
				Zen.fillRect(x * 10, y * 10, 10, 10);
			}

		}

	}
}
public static void randomize() {
	for (int x = 0; x < 50; x++) {
		for (int y = 0; y < 50; y ++) {
			grid[x][y] = Zen.flipCoin();

		}
	}

}




}

