# OpenGl.test

이번 주전자 과제를 하면서 OpenGL를 어떻게 활용하는지 어떤 프로그램을 사용하는지 알 수 있게 되어 좋았습니다. 
막힌 부분도 많았지만 찾아보고 어떻게 해결해야할지 스스로 발전할 수 있는 계기가 되었습니다.

![image](https://github.com/Joohawnee/OpenGl.test/assets/164468178/f3d449c1-d1e3-4c05-b74c-6cf4541d54c8)



#include <GL/freeglut.h>

// 회전 각도를 저장할 변수
float angleX = 0.0f, angleY = 0.0f;
int prevMouseX, prevMouseY;
bool isDragging = false;

void display() {
    glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);
    glLoadIdentity();
    gluLookAt(0.0, 0.0, 5.0, 0.0, 0.0, 0.0, 0.0, 1.0, 0.0);

    // 회전 적용
    glRotatef(angleX, 1.0, 0.0, 0.0);
    glRotatef(angleY, 0.0, 1.0, 0.0);

    glColor3f(3.0, 0.0, 1.0); // 주전자 색상 설정
    glutWireTeapot(1.0); // 3D 주전자 그리기

    glutSwapBuffers();
}

void reshape(int w, int h) {
    glViewport(0, 0, (GLsizei)w, (GLsizei)h);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluPerspective(45.0, (GLfloat)w / (GLfloat)h, 1.0, 200.0);
    glMatrixMode(GL_MODELVIEW);
}

void init() {
    glClearColor(0.0, 0.0, 0.0, 1.0);
    glEnable(GL_DEPTH_TEST);
}

// 마우스 이동 이벤트 처리 함수
void motion(int x, int y) {
    if (isDragging) {
        angleY += (x - prevMouseX);
        angleX += (y - prevMouseY);
        prevMouseX = x;
        prevMouseY = y;
        glutPostRedisplay();
    }
}

// 마우스 클릭 이벤트 처리 함수
void mouse(int button, int state, int x, int y) {
    if (button == GLUT_LEFT_BUTTON) {
        if (state == GLUT_DOWN) {
            isDragging = true;
            prevMouseX = x;
            prevMouseY = y;
        } else if (state == GLUT_UP) {
            isDragging = false;
        }
    }
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_DOUBLE | GLUT_RGB | GLUT_DEPTH);
    glutInitWindowSize(500, 500);
    glutInitWindowPosition(100, 100);
    glutCreateWindow("3D Teapot Simulation");
    init();
    glutDisplayFunc(display);
    glutReshapeFunc(reshape);
    glutMotionFunc(motion);
    glutMouseFunc(mouse);
    glutMainLoop();
    return 0;
}



